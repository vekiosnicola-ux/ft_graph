---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# ft_putchar

---
tags: [C09, magenta]
---

## Navigation
← C09_INDEX|C09 INDEX | [[Makefile|Next: Makefile →]]

## What it does
Writes a single character to standard output (stdout).

## The Insight
Uses the low-level `write` system call with file descriptor 1 (stdout) to output exactly one byte.

## Step-by-step Algorithm
1. Include `<unistd.h>` for the `write` function.
2. Call `write(1, &c, 1)` where `1` is stdout, `&c` is the address of the character, and `1` is the number of bytes to write.
3. Return (void).

## The Code
```c
 <unistd.h>  // Header for POSIX operating system API, provides write()

void ft_putchar(char c)  // Takes one character and outputs it to stdout
{
    write(1, &c, 1);  // System call: file descriptor 1 = stdout, &c = address of char, 1 = byte count
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 18 | `#include <unistd.h>` | Load theunistd header which defines the write() function |
| 20 | `void ft_putchar(char c)` | Function that outputs one character; returns nothing |
| 22 | `write(1, &c, 1);` | Call the write system call with: fd=1(stdout), pointer to c, send 1 byte |

## Common Traps
- ❌ Forgetting to include `<unistd.h>` (implicit declaration warning).
- ❌ Using `printf` instead of `write` (not allowed).
- ❌ Passing `c` directly instead of `&c` (write expects a pointer).

## Related Concepts
- 01_Concepts/write_syscall|write() syscall
- 07_Manual/c_unistd.h|unistd.h

## Related Exercises
- [[Makefile]]
- [[libft]]

How do you print a character with write?
::
`write(1, &c, 1)` - pass ADDRESS (&c), not value
