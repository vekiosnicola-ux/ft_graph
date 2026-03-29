---
tags: [C03, flashcard]
---


# ft_strcmp

## Navigation
← C03_INDEX|C03 INDEX | [[ft_strncmp|Next: ft_strncmp →]]

## What it does
Compares two strings lexicographically. Returns 0 if strings are equal, a positive value if s1 > s2, or a negative value if s1 < s2.

## Insight
Strings are compared character by character until a difference is found or the null terminator is reached. The difference between the first differing characters determines the result.

## Algorithm
1. Initialize index `i = 0`.
2. While `s1[i]` and `s2[i]` are not '\0' and `s1[i] == s2[i]`, increment `i`.
3. Return `s1[i] - s2[i]`.

## The Code (with pedagogical comments)
```c
int ft_strcmp(char *s1, char *s2)  // Function: returns int, takes two string pointers
{
    int i;  // Counter variable

    i = 0;  // Start at position 0
    while (s1[i] && s2[i] && s1[i] == s2[i])  // Loop while both chars exist and match
        i++;  // Move to next character
    return (s1[i] - s2[i]);  // Return difference at first mismatch
}
```

## Line-by-Line Translation
1. `int ft_strcmp(char *s1, char *s2)` - Define a function that returns an integer and takes two string pointers
2. `int i` - Declare a counter variable
3. `i = 0` - Start the counter at position 0
4. `while (s1[i] && s2[i] && s1[i] == s2[i])` - Keep looping while both characters exist and are equal
5. `i++` - Move to the next character
6. `return (s1[i] - s2[i])` - Return the difference between characters at the first mismatch

## Common Traps
- ❌ Not checking both strings for '\0' (would read past the end)
- ❌ Returning just `s1[i]` instead of `s1[i] - s2[i]` (should return difference)
- ❌ Forgetting to cast to unsigned when dealing with signed char differences

## Related Concepts
- 01_Concepts/null_terminator|Null Terminator
- 07_Manual/c_string.h|string.h

## Related Exercises
- [[ft_strncmp]]
- [[ft_strcat]]
- [[ft_strstr]]

## Propedeuticity
**Prerequisites:** [[ft_strlen]]
**Unlocks:** [[ft_strncmp]], [[ft_strstr]]

How does ft_strcmp work?
::
Compare characters one by one. Return difference at first mismatch. Return 0 if identical.
