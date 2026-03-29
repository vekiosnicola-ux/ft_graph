---
tags: [C04]
---


# ft_isalpha

## What it does
Returns 1 if the character is a letter (A-Z or a-z), otherwise returns 0.

## Insight
Letters have specific ASCII ranges: uppercase 65-90, lowercase 97-122. A character is alphabetic if it falls within either range.

## Algorithm
1. Check if `c` is between 'A' and 'Z' OR between 'a' and 'z'.
2. Return 1 if true, 0 otherwise.

## Code (with pedagogical comments)
```c
int ft_isalpha(int c)  // Function: returns 1 if c is a letter (A-Z or a-z), 0 otherwise
{
    if ((c >= 'A' && c <= 'Z') || (c >= 'a' && c <= 'z'))  // Check both uppercase and lowercase ranges
        return (1);  // c is uppercase OR lowercase letter, return true
    return (0);  // c is not a letter (digit, punctuation, etc.), return false
}
```

## Line-by-Line Translation
1. `int ft_isalpha(int c)` - Define a function that checks if a character is an alphabetic letter, returning 1 (true) or 0 (false)
2. `if ((c >= 'A' && c <= 'Z') || (c >= 'a' && c <= 'z')` - Check if c is in EITHER the uppercase range (65-90) OR the lowercase range (97-122)
3. `return (1);` - c matches one of the two letter ranges, so it's alphabetic
4. `return (0);` - c doesn't match either range (it's a digit, punctuation, space, etc.), so it's not alphabetic

## Common Traps
- ❌ Using `isalpha()` from `<ctype.h>` (not allowed).
- ❌ Forgetting to handle both upper and lowercase ranges.
- ❌ Using numeric values instead of character constants (e.g., 65 instead of 'A').

## Related Concepts
- ASCII Table - Understanding character encoding
- Character Ranges - Alphabetic characters span two separate ASCII ranges
- [[ft_isalnum]] - Combines alpha + digit checks
- [[ft_isdigit]] - Checks numeric characters only

## Propedeuticity
Part of the character classification family (C04). Prepares for `ft_strcapitalize`, `ft_strupcase`, `ft_strlowcase` in C02.
