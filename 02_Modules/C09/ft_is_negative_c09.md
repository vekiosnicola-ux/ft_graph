---
tags: [C09, magenta, flashcard]
date: 2026-03-29
status: complete
---
# ft_is_negative (C09)

## Navigation
← [[C09_Index|C09 INDEX]]

## What it does
Prints 'N' if the number is negative, 'P' if positive or zero. Part of `libft.a`.

## The Code
```c
#include <unistd.h>  // write()

void ft_is_negative(int n)  // Print N or P based on sign
{
    if (n < 0)               // Negative number
        write(1, "N", 1);   // Write 'N' to stdout
    else                     // Zero or positive
        write(1, "P", 1);   // Write 'P' to stdout
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 3 | `void ft_is_negative(int n)` | Takes an int, returns nothing |
| 5-6 | `if (n < 0) write(...)` | Negative → "N" |
| 7-8 | `else write(...)` | Zero or positive → "P" |

## Common Traps
- ❌ Treating 0 as negative — 0 is not negative, should print 'P'
- ❌ Printing newline — subject says no newline

## Related Exercises
- [[ft_putchar]]
- [[ft_putstr_c09]]
- [[libft]]

What does ft_is_negative print for 0?
::
'P' — zero is not negative, so it falls into the else branch.
