---
tags: [C00, flashcard]
---


# ft_putchar

## Navigation
← C00_INDEX|C00 INDEX | [[ft_print_alphabet|Next: ft_print_alphabet →]]

## What it does
Writes a single character to standard output (stdout).

## The Insight
Uses the low-level `write` system call with file descriptor 1 (stdout) to output exactly one byte. This is the foundation of all output in 42 - no `printf` allowed.

## Step-by-step Algorithm
1. Include `<unistd.h>` for the `write` function
2. Call `write(1, &c, 1)` where `1` is stdout, `&c` is the address of the character, and `1` is the number of bytes to write

## The Code (with pedagogical comments)
```c
 <unistd.h>  // Include library for system calls (write, read, close)

void    ft_putchar(char c)  // Function: takes one character as input
{
    write(1, &c, 1);  // Write 1 byte from address of c to stdout (fd=1)
}
```

## Line-by-Line Translation
1. `#include <unistd.h>` - Include the library that gives us access to system calls like write()
2. `void ft_putchar(char c)` - Define a function named ft_putchar that takes a character and returns nothing
3. `write(1, &c, 1)` - Write 1 byte from the memory address of c to file descriptor 1 (stdout)

## Common Traps
- ❌ Forgetting to include `<unistd.h>` (implicit declaration warning)
- ❌ Using `printf` instead of `write` (not allowed)
- ❌ Passing `c` directly instead of `&c` (write expects a pointer)
- ❌ Writing more than one byte

## Related Concepts
- 01_Concepts/write_syscall|write() syscall
- 07_Manual/c_unistd.h|unistd.h

## Related Exercises
- [[ft_print_alphabet]]
- [[ft_putstr]]

## Propedeuticity
**Prerequisites:** None (C00 is first C module)
**Unlocks:** All subsequent print/output exercises

How do you print a character with write?
::
`write(1, &c, 1)` - pass ADDRESS (&c), not value

## Dataview
```dataview
TABLE file.name as Exercise
FROM "02_Modules/C00"
SORT file.name ASC
```
