---
tags: [C02, flashcard]
---


# ft_strncpy

## What it does
Copies up to `n` characters from `src` to `dest`, padding with `\0` if src is shorter.

## The Insight
Copy while characters exist and we haven't reached n, then fill remainder with null bytes.

## Step-by-step Algorithm
1. Initialize `i = 0`
2. While `i < n` and `src[i] != '\0'`: copy
3. While `i < n`: set `dest[i] = '\0'`
4. Return `dest`

## The Code (with pedagogical comments)
```c
char *ft_strncpy(char *dest, char *src, unsigned int n)  // Function: returns pointer, takes two strings and n
{
    unsigned int i;  // Counter variable

    i = 0;  // Start at position 0
    while (i < n && src[i] != '\0')  // Copy while within n AND src has characters
    {
        dest[i] = src[i];  // Copy character from src to dest
        i++;  // Move to next position
    }
    while (i < n)  // If src ended before n, pad the rest with null bytes
    {
        dest[i] = '\0';  // Fill remaining space with null terminator
        i++;  // Move to next position
    }
    return (dest);  // Return the destination string
}
```

## Line-by-Line Translation
1. `char *ft_strncpy(char *dest, char *src, unsigned int n)` - Define a function that returns a string pointer and takes destination, source, and number of characters
2. `unsigned int i` - Declare an unsigned counter for indices
3. `i = 0` - Start at position 0
4. `while (i < n && src[i] != '\0')` - Loop while within n bytes AND source still has characters
5. `dest[i] = src[i]` - Copy one character from source to destination
6. `i++` - Move to the next position
7. `while (i < n)` - If we haven't filled all n positions
8. `dest[i] = '\0'` - Pad with null bytes
9. `i++` - Move to the next position
10. `return (dest)` - Return the destination pointer

## Common Traps
- ❌ Not padding with `\0` when src shorter than n
- ❌ Using `int` instead of `unsigned int` for n
- ❌ Forgetting to check src[i] != '\0' before copying

## Related Concepts
- 01_Concepts/null_terminator|Null Terminator
- [[ft_strcpy]]

## Related Exercises
- [[ft_strcpy]]
- [[ft_strlcpy]]

## Propedeuticity
**Prerequisites:** [[ft_strcpy]]
**Unlocks:** [[ft_strlcpy]]

How does strncpy differ from strcpy?
::
strncpy copies at most n characters and pads with null bytes if src is shorter than n.
