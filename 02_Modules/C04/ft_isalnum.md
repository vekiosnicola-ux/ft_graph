---
tags: [C04]
---


# ft_isalnum

## What it does
Returns 1 if the character is alphanumeric (A-Z, a-z, or 0-9), otherwise returns 0.

## Insight
A character is alphanumeric if it's either a letter (alpha) or a digit. Combine the ranges for both uppercase, lowercase, and digits.

## Algorithm
1. Check if `c` is between 'A' and 'Z' OR between 'a' and 'z' OR between '0' and '9'.
2. Return 1 if true, 0 otherwise.

## Code (with pedagogical comments)
```c
int ft_isalnum(int c)  // Function: returns 1 if c is alphanumeric (A-Z, a-z, or 0-9), 0 otherwise
{
    if ((c >= 'A' && c <= 'Z') || (c >= 'a' && c <= 'z') || (c >= '0' && c <= '9'))  // Check all three alphanumeric ranges
        return (1);  // c is uppercase OR lowercase OR a digit, return true
    return (0);  // c is not alphanumeric (punctuation, space, etc.), return false
}
```

## Line-by-Line Translation
1. `int ft_isalnum(int c)` - Define a function that checks if a character is alphanumeric (letter or digit), returning 1 (true) or 0 (false)
2. `if ((c >= 'A' && c <= 'Z') || (c >= 'a' && c <= 'z') || (c >= '0' && c <= '9'))` - Check if c is in ANY of three ranges: uppercase A-Z (65-90) OR lowercase a-z (97-122) OR digits 0-9 (48-57)
3. `return (1);` - c matches at least one of the three ranges, so it's alphanumeric
4. `return (0);` - c doesn't match any range, so it's not alphanumeric (it's punctuation, space, control char, etc.)

## Common Traps
- ❌ Using `isalnum()` from `<ctype.h>` (not allowed).
- ❌ Forgetting one of the three ranges (uppercase, lowercase, or digits).
- ❌ Using `||` instead of checking all three conditions.

## Related Concepts
- ASCII Table - Three separate ranges to check
- [[ft_isalpha]] - Letters only (parent function)
- [[ft_isdigit]] - Digits only (parent function)
- Character Classification - Part of the `<ctype.h>` family

## Propedeuticity
Combines `ft_isalpha` and `ft_isdigit`. Used in string validation functions like `ft_strcapitalize`.
