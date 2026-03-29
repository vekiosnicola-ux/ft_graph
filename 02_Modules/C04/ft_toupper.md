---
tags: [C04]
---


# ft_toupper

## What it does
Converts a lowercase letter to its uppercase equivalent. Returns the character unchanged if it's not a lowercase letter.

## Insight
Uppercase letters are exactly 32 positions before their lowercase counterparts in ASCII. Adding 32 to an uppercase letter makes it lowercase; subtracting 32 does the reverse.

## Algorithm
1. Check if `c` is between 'a' and 'z'.
2. If true, return `c - 32` (convert to uppercase).
3. Otherwise, return `c` unchanged.

## Code (with pedagogical comments)
```c
int ft_toupper(int c)  // Function: converts lowercase letter to uppercase, returns unchanged char otherwise
{
    if (c >= 'a' && c <= 'z')  // Check if c is a lowercase letter (a-z)
        return (c - 32);  // Convert to uppercase by subtracting 32 in ASCII
    return (c);  // c is not lowercase, return it unchanged
}
```

## Line-by-Line Translation
1. `int ft_toupper(int c)` - Define a function that converts a lowercase character to uppercase, returning an int (the converted character)
2. `if (c >= 'a' && c <= 'z')` - Check if the character `c` falls within the ASCII range for lowercase letters (97-122)
3. `return (c - 32);` - Subtract 32 from the ASCII value: 'a'(97)-32='A'(65), 'z'(122)-32='Z'(90) - this shifts lowercase to its uppercase equivalent
4. `return (c);` - If `c` was not a lowercase letter, return it unchanged (digits, uppercase, punctuation all pass through)

## Common Traps
- ❌ Using `toupper()` from `<ctype.h>` (not allowed).
- ❌ Using `c + 32` instead of `c - 32` (wrong direction).
- ❌ Not returning the original character if it's not lowercase.

## Related Concepts
- ASCII Table - 'A'=65, 'a'=97, difference is 32
- [[ft_tolower]] - Inverse operation (uppercase to lowercase)
- Case Conversion - Related to ft_strupcase/ft_strlowcase in C02

## Propedeuticity
Pair with `ft_tolower`. Both use the 32-offset trick. Together they prepare for string case conversion functions in C02.
