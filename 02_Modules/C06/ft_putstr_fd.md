---
tags: [C06]
---


# ft_putstr_fd

## What it Does
Outputs a string to the given file descriptor.

## The Insight
Iterate through the string and write each character using `write`.

## Step-by-step Algorithm
1. If `s` is NULL, return.
2. Initialize `i = 0`.
3. While `s[i] != '\0'`, write `s[i]` and increment `i`.

## The Code
```c
 <unistd.h> // Provides the write() function for low-level I/O operations

void ft_putstr_fd(char *s, int fd) // Function takes a string and a file descriptor
{                                 // fd: 1 = stdout, 2 = stderr, or other file descriptors
    int i;                        // Index variable to iterate through the string

    if (!s)                       // Guard clause: check if string pointer is NULL
        return;                   // Exit early to avoid undefined behavior (crash)
    i = 0;                        // Initialize index to 0 (start of string)
    while (s[i])                  // Loop while current character is not null terminator '\0'
    {                             // Shorter equivalent to: while (s[i] != '\0')
        write(fd, &s[i], 1);      // Write ONE character: address of s[i], count = 1 byte
        i++;                      // Move to the next character position
    }                             // Loop continues until '\0' is encountered
}                                 // Each character is written individually via write()
```

## Line-by-Line Translation
- `include <unistd.h>` — Include the header for the write() system call
- `void ft_putstr_fd(char *s, int fd)` — Define a function that writes a string to a file descriptor
- `int i;` — Declare an integer variable to track position in the string
- `if (!s)` — Check if the string pointer is NULL (defensive check)
- `return;` — Exit the function early if s is NULL
- `i = 0;` — Start at the first character of the string (index 0)
- `while (s[i])` — Continue looping while current character is not '\0' (null terminator)
- `write(fd, &s[i], 1);` — Write one byte: the current character, to the specified file descriptor
- `i++;` — Increment index to move to the next character

## Common Traps
- ❌ Not handling NULL string.
- ❌ Forgetting to check for NULL before iterating.
- ❌ Using `printf` instead of `write`.

## Related
- ex07 ft_putchar_fd
- ex09 ft_putendl_fd
- ex10 ft_putnbr_fd
