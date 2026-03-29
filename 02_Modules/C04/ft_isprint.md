---
tags: [C04]
---


# ft_isprint

## What it does
Returns 1 if the character is printable (ASCII 32-126), otherwise returns 0.

## Insight
Printable characters include space (32) through tilde (126). Non-printable characters are control characters (0-31) and DEL (127).

## Algorithm
1. Check if `c` is between 32 and 126 (inclusive).
2. Return 1 if true, 0 otherwise.

## Code (with pedagogical comments)
```c
int ft_isprint(int c)  // Function: returns 1 if c is printable (ASCII 32-126), 0 otherwise
{
    if (c >= 32 && c <= 126)  // Check if c is in the printable ASCII range
        return (1);  // c is printable (space through tilde), return true
    return (0);  // c is not printable (control char or DEL), return false
}
```

## Line-by-Line Translation
1. `int ft_isprint(int c)` - Define a function that checks if a character is printable, returning 1 (true) or 0 (false)
2. `if (c >= 32 && c <= 126)` - Check if c falls between ASCII 32 (space) and ASCII 126 (tilde) inclusive
3. `return (1);` - c is a printable character, return true
4. `return (0);` - c is either a control character (0-31), DEL (127), or outside range, return false

## Common Traps
- ❌ Using `isprint()` from `<ctype.h>` (not allowed).
- ❌ Off-by-one errors in the ASCII range check.
- ❌ Confusing with `ft_isascii` (which checks 0-127).

## Related Concepts
- ASCII Table - Printable range 32-126
- [[ft_isascii]] - Broader ASCII check (0-127)
- [[ft_putstr_non_printable]] - Uses isprint logic for filtering
- Character Classification - Part of the `<ctype.h>` family

## Propedeuticity
Used in `ft_putstr_non_printable` (C02) to distinguish printable from non-printable characters.
