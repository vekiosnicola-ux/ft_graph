---
tags: [C09, magenta, flashcard]
date: 2026-03-29
status: complete
---
# ft_strcmp (C09)

## Navigation
← [[C09_Index|C09 INDEX]] | [[ft_swap_c09|Next: ft_swap →]]

## What it does
Compares two strings character by character. Returns the difference between the first non-matching characters. Part of `libft.a`.

## The Code
```c
int ft_strcmp(char *s1, char *s2)  // Compare two strings
{
    int i;  // Index into both strings

    i = 0;
    while (s1[i] == s2[i] && s1[i] != '\0')  // While chars match and not at end
        i++;
    return (s1[i] - s2[i]);  // Return ASCII difference at divergence point
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 1 | `int ft_strcmp(char *s1, char *s2)` | Returns int: 0 if equal, negative if s1<s2, positive if s1>s2 |
| 6 | `while (s1[i] == s2[i] && s1[i] != '\0')` | Advance while matching and not end of string |
| 8 | `return (s1[i] - s2[i])` | Difference at first mismatch (or 0 if identical) |

## Common Traps
- ❌ Not checking for `'\0'` — would read past the string
- ❌ Returning 0/1/-1 instead of actual ASCII difference

## Related Exercises
- [[ft_strlen]]
- [[ft_strcpy]]
- [[libft]]

What does ft_strcmp return for "abc" vs "abd"?
::
Returns `'c' - 'd'` = `99 - 100` = `-1`. Negative means s1 comes before s2 lexicographically.
