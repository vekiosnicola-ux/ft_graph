---
tags: [C03]
---


# ft_strncmp

## What it does
Compares up to `n` characters of two strings lexicographically. Returns 0 if equal, positive if s1 > s2, negative if s1 < s2.

## Insight
Same as strcmp but stops after `n` characters. Comparison stops early if a null terminator is encountered before `n`.

## Algorithm
1. Initialize index `i = 0`.
2. While `i < n` and `s1[i]` and `s2[i]` are not '\0' and `s1[i] == s2[i]`, increment `i`.
3. If `i == n`, return 0.
4. Return `s1[i] - s2[i]`.

## Code (with pedagogical comments)
```c
int ft_strncmp(char *s1, char *s2, unsigned int n)  // Function: compares up to n chars of s1 and s2
{
    unsigned int i;  // Counter for how many characters we've compared

    i = 0;  // Start comparing from position 0
    while (i < n && s1[i] && s2[i] && s1[i] == s2[i])  // While: within n limit AND both chars exist AND chars match
        i++;  // Move to next character position
    if (i == n)  // If we compared n characters without difference
        return (0);  // They match as far as we could check, return 0
    return (s1[i] - s2[i]);  // Return the difference between the first mismatched characters
}
```

## Line-by-Line Translation
1. `int ft_strncmp(char *s1, char *s2, unsigned int n)` - Define a function that compares the first `n` characters of `s1` and `s2`, returning their difference
2. `unsigned int i;` - Declare an unsigned counter to track position in the strings
3. `i = 0;` - Begin comparison at the first character
4. `while (i < n && s1[i] && s2[i] && s1[i] == s2[i])` - Loop while: we haven't exceeded n, both strings have characters at position i, AND the characters are equal
5. `i++;` - Advance to the next character position
6. `if (i == n)` - Check if we exhausted our comparison limit of n characters
7. `return (0);` - All n characters compared equally, return 0 (strings are "equal" for first n)
8. `return (s1[i] - s2[i]);` - Return the ASCII difference at the first position where characters differed (positive if s1 > s2, negative if s1 < s2)

## Common Traps
- ❌ Using `int` instead of `unsigned int` for `n`.
- ❌ Not handling `n == 0` (should return 0 without comparing).
- ❌ Forgetting that comparison stops at '\0' before reaching `n`.

## Related Concepts
- [[ft_strcmp]] - Full string comparison
- String Handling - Memory as byte arrays
- [[ft_strlcat]] - Safe string concatenation

## Propedeuticity
Builds on [[ft_strcmp]] knowledge. Essential for understanding safe string comparison before [[ft_strstr]] and [[ft_strlcat]].
