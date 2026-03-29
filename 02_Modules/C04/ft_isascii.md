---
tags: [C04]
---


# ft_isascii

## What it does
Returns 1 if the character is a valid ASCII character (0-127), otherwise returns 0.

## Insight
ASCII characters are 8-bit values from 0 to 127. A simple range check is sufficient.

## Algorithm
1. Check if `c` is between 0 and 127 (inclusive).
2. Return 1 if true, 0 otherwise.

## Code (with pedagogical comments)
```c
int ft_isascii(int c)  // Function: returns 1 if c is a valid ASCII character (0-127), 0 otherwise
{
    if (c >= 0 && c <= 127)  // Check if c is in the 7-bit ASCII range
        return (1);  // c is ASCII (0-127), return true
    return (0);  // c is outside ASCII range (negative or >127), return false
}
```

## Line-by-Line Translation
1. `int ft_isascii(int c)` - Define a function that checks if a character is a valid ASCII character, returning 1 (true) or 0 (false)
2. `if (c >= 0 && c <= 127)` - Check if c falls between ASCII 0 and ASCII 127 inclusive (standard 7-bit ASCII range)
3. `return (1);` - c is a valid ASCII character, return true
4. `return (0);` - c is outside the ASCII range (negative values like -1 or bytes > 127), return false

## Common Traps
- ❌ Using `isascii()` from `<ctype.h>` (not allowed).
- ❌ Forgetting that negative values are not ASCII.
- ❌ Using char type instead of int for the parameter.

## Related Concepts
- ASCII Table - Full 0-127 range
- Character Classification - Part of the `<ctype.h>` family
- [[ft_isprint]] - Printable subset of ASCII (32-126)

## Propedeuticity
Simplest of the character classification functions. ASCII is foundational for understanding character encoding in C.
