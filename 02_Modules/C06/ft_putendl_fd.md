---
tags: [C06]
---


# ft_putendl_fd

## What it Does
Outputs a string followed by a newline to the given file descriptor.

## The Insight
Write the string, then write '\n'.

## Step-by-step Algorithm
1. If `s` is NULL, return.
2. Write the string using `ft_putstr_fd`.
3. Write '\n'.

## The Code
```c
 <unistd.h> // Provides the write() function for low-level I/O operations

void ft_putendl_fd(char *s, int fd) // Function takes a string and file descriptor
{                                  // fd = 1 for stdout, 2 for stderr, etc.
    if (!s)                        // Check if the string pointer is NULL (null check)
        return;                    // Safety first: do nothing if s is NULL
    while (*s)                     // Loop through each character until null terminator '\0'
    {
        write(fd, s, 1);           // Write one character at a time to the file descriptor
        s++;                       // Move pointer to the next character in the string
    }                              // Loop ends when *s == '\0' (null terminator)
    write(fd, "\n", 1);            // After the string, write a newline character to fd
}                                  // Result: "string\n" appears in the output
```

## Line-by-Line Translation
- `include <unistd.h>` — Include the header for the write() system call
- `void ft_putendl_fd(char *s, int fd)` — Define a function that writes a string plus newline to a file descriptor
- `if (!s)` — Check if the string pointer is NULL (defensive programming)
- `return;` — Exit early if string is NULL (avoid crash)
- `while (*s)` — Loop while the current character is not the null terminator '\0'
- `write(fd, s, 1);` — Write one byte: the current character, to the file descriptor
- `s++;` — Move the pointer forward to the next character in the string
- `write(fd, "\n", 1);` — Write the newline character after the string ends

## Related
- ex07 ft_putchar_fd
- ex08 ft_putstr_fd
- ex10 ft_putnbr_fd
