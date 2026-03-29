---
tags: [C06]
---


# ft_putchar_fd

## What it Does
Outputs a character to the given file descriptor.

## The Insight
Uses `write` syscall with the address of the character.

## Step-by-step Algorithm
1. Call `write(fd, &c, 1)`.

## The Code
```c
 <unistd.h> // Include header for write() - the low-level I/O system call

void ft_putchar_fd(char c, int fd) // Function takes a char and a file descriptor
{                                  // fd (file descriptor): 0=stdin, 1=stdout, 2=stderr
    write(fd, &c, 1);              // write() needs an ADDRESS (&c), not the value
}                                  // write outputs exactly 1 byte from memory address &c
```

## Line-by-Line Translation
- `include <unistd.h>` — Include the Unix standard header for system calls like write()
- `void ft_putchar_fd(char c, int fd)` — Define a function that outputs one character to a file descriptor
- `write(fd, &c, 1);` — System call: write 1 byte from the address of c to file descriptor fd

## Common Traps
- ❌ Forgetting to pass `&c` (address of character).
- ❌ Using `printf` instead of `write`.

## Related
- ex08 ft_putstr_fd
- ex09 ft_putendl_fd
- ex10 ft_putnbr_fd
