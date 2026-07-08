---
tags: [C09, magenta, flashcard]
date: 2026-03-29
status: complete
---
# ft_swap (C09)

## Navigation
← [[C09_Index|C09 INDEX]] | [[ft_putstr_c09|Next: ft_putstr →]]

## What it does
Swaps two integer values using pointers. Part of `libft.a`.

## The Code
```c
void ft_swap(int *a, int *b)  // Swap values at two addresses
{
    int tmp;  // Temporary storage

    tmp = *a;   // Save value at address a
    *a = *b;    // Overwrite a with b's value
    *b = tmp;   // Set b to saved value
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 1 | `void ft_swap(int *a, int *b)` | Takes pointers to two ints |
| 5 | `tmp = *a;` | Dereference: save the value a points to |
| 6 | `*a = *b;` | Copy value of b into a |
| 7 | `*b = tmp;` | Copy saved value into b |

## Common Traps
- ❌ Swapping pointers instead of values: `a = b` vs `*a = *b`
- ❌ Missing temp variable: `*a = *b; *b = *a;` destroys original *a

## Related Exercises
- [[ft_putchar]]
- [[ft_strlen]]
- [[libft]]
- [[pointers]]

Why does ft_swap need pointers?
::
C passes arguments by value. Without pointers, the function would swap local copies and the caller's variables would be unchanged. Pointers let you modify the caller's memory.
