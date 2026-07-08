---
tags: [C09, magenta, flashcard]
date: 2026-03-29
status: complete
---
# ft_putstr (C09)

## Navigation
← [[C09_Index|C09 INDEX]] | [[ft_is_negative_c09|Next: ft_is_negative →]]

## What it does
Writes a string to standard output. Part of `libft.a`.

## The Code
```c
#include <unistd.h>  // write()

void ft_putstr(char *str)  // Print a string to stdout
{
    int i;  // String index

    i = 0;
    while (str[i] != '\0')      // Walk until null terminator
    {
        write(1, &str[i], 1);   // Write one character to stdout (fd 1)
        i++;
    }
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 1 | `#include <unistd.h>` | For write() system call |
| 3 | `void ft_putstr(char *str)` | Takes string, no return value |
| 8 | `while (str[i] != '\0')` | Iterate until end of string |
| 10 | `write(1, &str[i], 1);` | Write single byte to fd 1 (stdout) |

## Common Traps
- ❌ Using printf — only write() is allowed
- ❌ Not handling empty string (works: loop never entered)

## Related Exercises
- [[ft_putchar]]
- [[ft_strlen]]
- [[libft]]
- [[write_syscall]]

How does ft_putstr differ from ft_putchar?
::
`ft_putchar` writes a single character. `ft_putstr` loops through an entire string, calling write for each character until `'\0'`.
