---
tags: [C04]
---


# ft_isdigit

## What it does
Returns 1 if the character is a digit (0-9), otherwise returns 0.

## Insight
Digits are consecutive in ASCII: '0' is 48, '9' is 57. A character is a digit if it falls within this range.

## Algorithm
1. Check if `c` is between '0' and '9'.
2. Return 1 if true, 0 otherwise.

## Code (with pedagogical comments)
```c
int ft_isdigit(int c)  // Function: returns 1 if c is a digit (0-9), 0 otherwise
{
    if (c >= '0' && c <= '9')  // Check if c is in the ASCII digit range
        return (1);  // c is between '0' and '9', return true
    return (0);  // c is not a digit, return false
}
```

## Line-by-Line Translation
1. `int ft_isdigit(int c)` - Define a function that checks if a character is a decimal digit, returning 1 (true) or 0 (false)
2. `if (c >= '0' && c <= '9')` - Check if c falls within the ASCII range for digits: '0' (48) through '9' (57) inclusive
3. `return (1);` - c is a digit character ('0', '1', ..., '9'), return true
4. `return (0);` - c is not a digit (letter, punctuation, space, etc.), return false

## Common Traps
- ❌ Using `isdigit()` from `<ctype.h>` (not allowed).
- ❌ Using numeric values instead of character constants.
- ❌ Confusing with `isalnum` (which includes letters).

## Related Concepts
- ASCII Table - Digits 48-57 are consecutive
- Character Ranges - Single contiguous range for digits
- [[ft_isalnum]] - Combines alpha + digit checks
- [[ft_atoi]] - Uses digit checking for string conversion

## Propedeuticity
Essential for `ft_atoi` conversion function. Digits must be distinguished from other characters during numeric conversion.
