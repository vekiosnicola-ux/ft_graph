---
tags: [C04]
---


# ft_tolower

## What it does
Converts an uppercase letter to its lowercase equivalent. Returns the character unchanged if it's not an uppercase letter.

## Insight
Lowercase letters are exactly 32 positions after their uppercase counterparts in ASCII. Subtracting 32 from a lowercase letter makes it uppercase; adding 32 does the reverse.

## Algorithm
1. Check if `c` is between 'A' and 'Z'.
2. If true, return `c + 32` (convert to lowercase).
3. Otherwise, return `c` unchanged.

## Code (with pedagogical comments)
```c
int ft_tolower(int c)  // Function: converts uppercase letter to lowercase, returns unchanged char otherwise
{
    if (c >= 'A' && c <= 'Z')  // Check if c is an uppercase letter (A-Z)
        return (c + 32);  // Convert to lowercase by adding 32 in ASCII
    return (c);  // c is not uppercase, return it unchanged
}
```

## Line-by-Line Translation
1. `int ft_tolower(int c)` - Define a function that converts an uppercase character to lowercase, returning an int (the converted character)
2. `if (c >= 'A' && c <= 'Z')` - Check if the character `c` falls within the ASCII range for uppercase letters (65-90)
3. `return (c + 32);` - Add 32 to the ASCII value: 'A'(65)+32='a'(97), 'Z'(90)+32='z'(122) - this shifts uppercase to its lowercase equivalent
4. `return (c);` - If `c` was not an uppercase letter, return it unchanged (digits, lowercase, punctuation all pass through)

## Common Traps
- ❌ Using `tolower()` from `<ctype.h>` (not allowed).
- ❌ Using `c - 32` instead of `c + 32` (wrong direction).
- ❌ Not returning the original character if it's not uppercase.

## Related Concepts
- ASCII Table - 'A'=65, 'a'=97, difference is 32
- [[ft_toupper]] - Inverse operation (lowercase to uppercase)
- Case Conversion - Related to ft_strupcase/ft_strlowcase in C02

## Propedeuticity
Pair with `ft_toupper`. Both use the 32-offset trick. Together they prepare for string case conversion functions in C02.
