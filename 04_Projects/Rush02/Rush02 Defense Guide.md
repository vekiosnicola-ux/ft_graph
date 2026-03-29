---
tags: [defense, rush, rush02]
date: 2026-03-29
status: complete
---
# Rush02 Defense Guide — Line-by-Line Annotations
**Tags:** #42piscine   

> [!TIP]
> This file is your study guide for the evaluation. Comments can't go in the actual source files (they'd break the 25-line Norm limit), so everything is documented here.

---
ins
## 1. `includes/rush02.h` — The Header

```c
 RUSH02_H              // If RUSH02_H hasn't been defined yet...
# define RUSH02_H             // ...define it now (prevents double-include)

# include <stdlib.h>          // For malloc() and free()
# include <unistd.h>          // For write(), read(), close()
# include <fcntl.h>           // For open() and O_RDONLY flag

# define DICT_DEFAULT "numbers.dict"  // Default dictionary filename
```

**Plain English:** This is our "table of contents." It tells every `.c` file what functions exist, what libraries we use, and where to find the default dictionary. The `#ifndef` guard prevents the compiler from reading this file twice if two `.c` files both `#include` it.

---

## 2. `srcs/main.c` — The Entry Point

```c
static int  print_error(char *msg)      // Prints an error message to STDERR
{
    while (*msg)                         // Loop through every character in msg
        write(2, msg++, 1);             // Write 1 char to fd 2 (STDERR), advance pointer
    return (1);                          // Return 1 = "something went wrong"
}
```
**Plain English:** This is our error printer. It writes to file descriptor 2 (standard error, NOT standard output). This matters because evaluators might redirect stdout to check only the number output — errors must go to a separate channel.

```c
int  main(int argc, char **argv)
{
    char  *dict;                         // Will hold the entire dictionary file as one string
    char  *num_str;                      // Will point to the cleaned number string

    if (argc < 2 || argc > 3)           // Must have 1 or 2 args (+ program name)
        return (print_error("Error\n")); // Wrong arg count = immediate error
    num_str = argv[1];                   // Default: first arg is the number
    if (argc == 3)                       // If 2 args given:
        num_str = argv[2];               //   second arg is the number
    num_str = validate_input(num_str);   // Clean & validate the number string
    if (!num_str)                        // If validation failed (letters, negative, etc.)
        return (print_error("Error\n"));
    if (argc == 3)                       // If custom dict was provided:
        dict = read_file(argv[1]);       //   load that file
    else
        dict = read_file(DICT_DEFAULT);  //   otherwise load "numbers.dict"
    if (!dict)                           // If file couldn't be opened/read
        return (print_error("Dict Error\n"));
    if (!convert_number(dict, num_str))  // Try to convert — returns 0 on failure
    {
        free(dict);                      // Clean up the buffer before exiting
        return (print_error("Dict Error\n"));
    }
    free(dict);                          // Success path: clean up the buffer
    return (0);                          // Exit code 0 = success
}
```
**Plain English:** This is the control tower. It checks how many arguments we got, decides which one is the number and which is the dictionary path, validates the number, loads the dictionary file into a single string in memory, and then asks `convert_number` to do the translation. If anything fails, it prints the appropriate error. At the end, it frees the one malloc'd buffer.

---

## 3. `srcs/validation.c` — Input Checking

```c
static int  is_digit(char c)             // Checks if a character is 0-9
{
    return (c >= '0' && c <= '9');        // ASCII: '0'=48, '9'=57
}

static int  is_space(char c)             // Checks all 6 types of whitespace
{
    return (c == ' ' || c == '\t' || c == '\n' || c == '\v'
        || c == '\f' || c == '\r');       // space, tab, newline, vtab, formfeed, carriage return
}
```
**Plain English:** Helper functions. `is_digit` returns 1 (true) if the character is a number. `is_space` returns 1 if the character is any kind of invisible whitespace — not just the spacebar, but also tabs, newlines, etc.

```c
char  *validate_input(char *str)
{
    char  *num_start;                    // Will mark where the actual number begins

    while (is_space(*str))               // Skip leading whitespace
        str++;
    if (*str == '+')                     // Allow optional "+" sign (e.g., "+42")
        str++;
    if (!*str || !is_digit(*str))        // If nothing left, or first char isn't a digit
        return (NULL);                   //   → invalid input
    while (*str == '0' && *(str + 1))    // Skip leading zeros: "00042" → "42"
        str++;                           //   but keep at least one char ("0" stays "0")
    num_start = str;                     // Mark this position — this is our clean number
    while (*str)                         // Walk through the rest
    {
        if (!is_digit(*str))             // If ANY remaining char is not a digit
            return (NULL);               //   → invalid (e.g., "42abc")
        str++;
    }
    return (num_start);                  // Return pointer to the clean number string
}
```
**Plain English:** This function cleans the user's input. It strips whitespace and an optional `+`, removes excess leading zeros, and then checks that every single remaining character is a digit. If anything is wrong, it returns NULL (which triggers "Error\n" in main). Crucially, it returns a **pointer into the original argv string** — no malloc needed here.

---

## 4. `srcs/scan_dict.c` — Dictionary Lookup (No Linked List!)

```c
static char  *try_match(char *line, char *key)
{
    int  i;

    i = 0;
    while (key[i] && line[i] == key[i])  // Compare key chars against start of line
        i++;
    if (key[i] != '\0')                  // If we didn't reach end of key → no match
        return (NULL);
    while (line[i] == ' ')               // Skip spaces between number and colon
        i++;
    if (line[i] != ':')                  // Not a colon → this line doesn't match format
        return (NULL);
    i++;                                 // Skip past the colon
    while (line[i] == ' ')               // Skip spaces between colon and value
        i++;
    return (line + i);                   // Return pointer to where the value text begins
}
```
**Plain English:** Given a position in the buffer and a key like `"42"`, this checks if the line starts with exactly `"42"` followed by optional spaces and a colon. If yes, it returns a pointer to the value text (e.g., pointing to `"forty-two\n..."`). If no, it returns NULL and we move on.

**Why this prevents false matches:** If the dict has `"100: hundred"` and we search for `"10"`, after matching `"10"`, the next character in the line is `"0"` (not a space or colon), so it correctly returns NULL.

```c
static char  *extract_val(char *start)
{
    int  len;

    len = 0;
    while (start[len] && start[len] != '\n')  // Count chars until newline or end
        len++;
    while (len > 0 && start[len - 1] == ' ')  // Trim trailing spaces from value
        len--;
    return (ft_substr(start, 0, len));         // Return a malloc'd copy of the value
}
```
**Plain English:** Once `try_match` found where the value starts, this function measures its length (up to the newline), trims trailing spaces, and returns a fresh malloc'd copy of just the value string. The caller must `free()` this.

```c
char  *get_val(char *buf, char *key)
{
    char  *match;

    while (*buf)                               // Loop through the entire buffer
    {
        while (*buf == '\n' || *buf == ' ')    // Skip empty lines and leading spaces
            buf++;
        if (!*buf)                             // Reached end of buffer
            break ;
        match = try_match(buf, key);           // Try to match this line against our key
        if (match)                             // Found it!
            return (extract_val(match));       //   Extract and return the value
        while (*buf && *buf != '\n')           // No match — skip rest of this line
            buf++;
        if (*buf == '\n')                      // Move past the newline to the next line
            buf++;
    }
    return (NULL);                             // Key not found anywhere in the dict
}
```
**Plain English:** This is our "search engine." It walks through the entire dictionary buffer line by line, trying to match each line against the requested key. When it finds a match, it extracts the value. If it reaches the end without finding anything, it returns NULL (which cascades to "Dict Error\n").

---

## 5. `srcs/file_utils.c` — File I/O & String Helpers

```c
char  *ft_strdup(char *str)              // Makes a malloc'd copy of a string
{
    char  *dup;
    int    i;

    if (!str)                            // Safety: don't crash on NULL
        return (NULL);
    dup = malloc(sizeof(char) * (ft_strlen(str) + 1));  // +1 for '\0'
    if (!dup)                            // malloc failed
        return (NULL);
    i = -1;
    while (str[++i])                     // Copy each character (pre-increment trick)
        dup[i] = str[i];
    dup[i] = '\0';                       // Null-terminate the copy
    return (dup);
}
```
**Plain English:** This is our version of the standard `strdup()` — we can't use `<string.h>`. It measures the string, mallocs that exact size plus one byte for the null terminator, copies every character, and returns the new string.

```c
char  *ft_substr(char *s, unsigned int start, unsigned int len)
```
**Plain English:** Extracts a substring from position `start` with length `len`. Used by `extract_val` in `scan_dict.c` to carve out just the value portion from the big buffer. Returns a malloc'd copy.

```c
static int  get_file_size(char *filename)
{
    int    fd;
    int    size;
    int    ret;
    char   buf[1024];                    // Temporary buffer (on the stack, not malloc'd)

    size = 0;
    fd = open(filename, O_RDONLY);       // Open file for reading
    if (fd < 0)                          // File doesn't exist or can't be opened
        return (-1);
    ret = read(fd, buf, 1024);           // Read first batch of up to 1024 bytes
    while (ret > 0)                      // Keep reading until EOF (ret == 0) or error
    {
        size += ret;                     // Accumulate total bytes read
        ret = read(fd, buf, 1024);       // Read next batch
    }
    close(fd);                           // Close the file descriptor
    return (size);                       // Return total size in bytes
}
```
**Plain English:** We need to know how big the file is BEFORE we malloc the buffer. Since we can't use `fstat` or `lseek` (not in allowed functions), we read the entire file in 1024-byte chunks just to count the bytes, then close it. Yes, this means we open the file twice — but it's the simplest approach with only `open/read/close` available.

```c
char  *read_file(char *filename)
```
**Plain English:** Opens the file a second time, mallocs exactly `size + 1` bytes, reads the entire file into that buffer, null-terminates it, and returns it. This single buffer IS the dictionary for the entire lifetime of the program. One `free(dict)` at the end cleans up everything.

---

## 6. `srcs/print_utils.c` — Output Functions

```c
void  ft_putchar(char c)                 // Writes exactly 1 character to stdout
{
    write(1, &c, 1);                     // fd 1 = standard output
}

void  ft_putstr(char *str)               // Writes a full string to stdout
{
    if (!str)                            // Safety: don't crash on NULL pointer
        return ;
    while (*str)                         // Walk through each character
    {
        ft_putchar(*str);                // Print it via ft_putchar (proper function reuse)
        str++;                           // Advance to next character
    }
}
```
**Plain English:** Since we can't use `printf`, these are our output tools. `ft_putchar` writes one character at a time using the `write` system call. `ft_putstr` loops through a string and calls `ft_putchar` for each character.

```c
int  ft_strcmp(char *s1, char *s2)
```
**Plain English:** Compares two strings character by character. Returns 0 if they're identical, nonzero if they differ. We use this everywhere — checking if a chunk is `"000"` (all zeros), comparing dict keys, etc. The `unsigned char` cast at the end prevents negative comparisons on extended ASCII.

---

## 7. `srcs/convert.c` — The Chunking Engine

```c
static void  get_chunk(char *num, int len, int *chunk_len, char *chunk)
```
**Plain English:** Given the number `"123456"` (length 6), this calculates `6 % 3 = 0`, so the first chunk is 3 digits: `"123"`. For `"12345"` (length 5), `5 % 3 = 2`, so the first chunk is 2 digits: `"12"`. It copies those digits into the `chunk` buffer.

```c
static char  *get_magnitude(int zeros)
```
**Plain English:** Builds a string like `"1000"` (3 zeros) or `"1000000"` (6 zeros) dynamically using malloc. This string is then looked up in the dictionary to find the word "thousand" or "million".

```c
static int  print_magnitude(char *dict, int len, int chunk_len)
{
    int    zeros;
    char  *mag;                          // The magnitude string ("1000", etc.)
    char  *val;                          // The word from the dictionary ("thousand", etc.)

    zeros = len - chunk_len;             // How many digits remain after this chunk
    if (zeros > 0)                       // If there ARE remaining digits (not the last chunk)
    {
        mag = get_magnitude(zeros);      // Build "1" followed by `zeros` zeroes
        if (!mag)
            return (0);
        val = get_val(dict, mag);        // Look up e.g. "1000" → "thousand"
        free(mag);                       // Done with the magnitude string
        if (!val)                        // Dict doesn't have this magnitude
            return (0);                  //   → triggers Dict Error
        ft_putstr(" ");                  // Space before "thousand"
        ft_putstr(val);                  // Print "thousand"
        free(val);                       // Free the malloc'd value from get_val
    }
    return (1);                          // Success
}
```
**Plain English:** After printing a chunk like "one hundred twenty three", this checks if we need a magnitude word. If the original number had 6 digits and this chunk was 3, there are 3 remaining digits, so we need "thousand" (10^3 = 1000). We dynamically build `"1000"` and search for it in the dictionary.

```c
int  convert_number(char *dict, char *num)
```
**Plain English:** The main loop. For input `"123456789"` (9 digits):
1. First chunk: `"123"` (9 % 3 = 0, so take 3). Print it. Magnitude = 10^6 = "million"
2. Second chunk: `"456"`. Print it. Magnitude = 10^3 = "thousand"  
3. Third chunk: `"789"`. Print it. No magnitude (last chunk).
4. Print `"\n"`. Done!

---

## 8. `srcs/core_logic.c` — Translating Digits to Words

```c
static int  print_single(char *dict, char *chunk)
```
**Plain English:** The simplest case. Takes a key like `"5"`, searches the dictionary, prints `"five"`, frees the malloc'd result. Returns 0 if the key wasn't found.

```c
static int  print_tens(char *dict, char *chunk)
{
    char   key[3];                       // Stack buffer for building keys like "40"
    char  *val;                          // Pointer for exact-match lookup

    if (chunk[0] == '0')                 // Tens digit is zero → just print the units
        return (print_single(dict, chunk + 1));
    val = get_val(dict, chunk);          // TRY EXACT MATCH FIRST (e.g., "42" → "l'ecole")
    if (val)                             // Found an exact entry in the dict!
    {
        ft_putstr(val);                  // Print it directly
        free(val);                       // Free the malloc'd copy
        return (1);                      // Done — no decomposition needed
    }
    // No exact match → decompose into tens + units
    key[0] = chunk[0];                   // Take the tens digit (e.g., '4')
    key[1] = '0';                        // Append '0' to make "40"
    key[2] = '\0';                       // Null-terminate
    if (!print_single(dict, key))        // Print "forty"
        return (0);
    if (chunk[1] != '0')                 // If units digit isn't zero
    {
        key[0] = chunk[1];              // Take the units digit (e.g., '2')
        key[1] = '\0';                  // Make it a single-char string
        return (print_single(dict, key));// Print "two"
    }
    return (1);
}
```
**Plain English:** This handles 2-digit numbers. FIRST it checks if the dictionary has an exact entry for the full 2-digit number (like `"42: l'ecole"`). If yes, it uses that directly. If not, it splits: looks up `"40"` → prints `"forty"`, then looks up `"2"` → prints `"two"`. This exact-match-first approach is critical because the subject says dictionary values can be customized.

```c
static int  print_hundreds(char *dict, char *chunk)
```
**Plain English:** For a 3-digit chunk like `"342"`: extracts `"3"` → prints `"three"`, prints a space, looks up `"100"` → prints `"hundred"`, then (if tens/units aren't both zero) adds a space for whatever comes next.

```c
int  print_chunk(char *dict, char *chunk, int len)
```
**Plain English:** The dispatcher. Routes to `print_single` (1 digit), `print_tens` (2 digits), or `print_hundreds` + `print_tens` (3 digits) based on chunk length.

---

## 9. `Makefile` — Build System

```makefile
NAME     = rush-02              # Final executable name
CC       = cc                   # Compiler (as required by subject)
CFLAGS   = -Wall -Wextra -Werror  # All warnings ON, warnings = errors

SRCS     = srcs/main.c srcs/validation.c srcs/scan_dict.c \
           srcs/convert.c srcs/print_utils.c srcs/file_utils.c \
           srcs/core_logic.c       # All 7 source files
OBJS     = ${SRCS:.c=.o}          # Replace .c with .o for object files

all:     ${NAME}                  # Default target: build everything
.c.o:    ...                      # Rule: compile each .c to .o with our flags
${NAME}: ${OBJS}                  # Link all .o files into the final executable
clean:   rm -f ${OBJS}            # Delete object files only
fclean:  clean + rm -f ${NAME}    # Delete object files AND the executable
re:      fclean all               # Full rebuild from scratch
.PHONY:  all clean fclean re      # These targets aren't real files
```
**Plain English:** The Makefile is a recipe book for the compiler. `make` builds the program, `make clean` removes intermediate `.o` files, `make fclean` removes everything, and `make re` does a full clean rebuild. The `-Werror` flag means any compiler warning is treated as a fatal error.

---

## Memory Model Summary

```
Program Start
  └─ main() calls read_file()
       └─ malloc #1: the entire dictionary buffer (e.g., 400 bytes)
  
During Conversion (per lookup):
  └─ get_val() calls extract_val()
       └─ malloc #2: small value string (e.g., "forty", 6 bytes)
       └─ Immediately free'd after ft_putstr() prints it
  
  └─ get_magnitude() in convert.c
       └─ malloc #3: magnitude string (e.g., "1000", 5 bytes)
       └─ Immediately free'd after get_val() uses it

Program End
  └─ free(dict): releases malloc #1
  └─ Exit with code 0 (success) or 1 (error)

Total persistent allocations: 1 (the dict buffer)
Total temporary allocations: ~10-20 per number (all freed immediately)
Memory leaks: 0
```
