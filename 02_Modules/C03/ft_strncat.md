---
tags: [C03]
---


# ft_strncat

## What it does
Appends up to `n` characters from `src` to `dest`, overwriting '\0' and adding a new '\0' at the end. Returns `dest`.

## Insight
Same as strcat but only copies up to `n` characters from src. Handles the case where src is shorter than n.

## Algorithm
1. Find the index `i` where `dest[i] == '\0'`.
2. Initialize `j = 0`.
3. While `j < n` and `src[j] != '\0'`, set `dest[i + j] = src[j]` and increment `j`.
4. Set `dest[i + j] = '\0'`.
5. Return `dest`.

## Code (with pedagogical comments)
```c
char *ft_strncat(char *dest, char *src, int n)  // Function: appends up to n chars from src to dest
{
    int i;  // Index for finding end of dest
    int j;  // Index for copying from src

    i = 0;  // Start at beginning of dest
    while (dest[i] != '\0')  // Loop until we find the null terminator (end of dest)
        i++;  // Move forward until dest[i] is '\0'
    j = 0;  // Start copying from beginning of src
    while (j < n && src[j] != '\0')  // Copy up to n chars, but stop if src ends first
    {
        dest[i + j] = src[j];  // Copy character from src to end of dest
        j++;  // Advance in both src and our position in result
    }
    dest[i + j] = '\0';  // Always null-terminate the concatenated string
    return (dest);  // Return pointer to the beginning of dest
}
```

## Line-by-Line Translation
1. `char *ft_strncat(char *dest, char *src, int n)` - Define a function that appends at most `n` characters from `src` to `dest`, returning `dest`
2. `int i; int j;` - Declare two integer counters: `i` tracks position in dest, `j` tracks position in src
3. `i = 0;` - Start searching for dest's end from position 0
4. `while (dest[i] != '\0')` - Keep moving forward until we find where dest ends
5. `i++;` - Advance one position at a time
6. `j = 0;` - Start copying src from its first character
7. `while (j < n && src[j] != '\0')` - Copy characters while we haven't reached `n` limit AND src still has characters
8. `dest[i + j] = src[j];` - Place src character at the end of dest (i puts us at end, j tracks offset)
9. `j++;` - Move to next character in src
10. `dest[i + j] = '\0';` - After copying, place null terminator to properly end the combined string
11. `return (dest);` - Return the original dest pointer (not the modified position)

## Common Traps
- ❌ Using `unsigned int` for `n` instead of `int` (depending on the original signature).
- ❌ Forgetting that src might be shorter than `n` (must check `src[j] != '\0'`).
- ❌ Not adding '\0' after copying.

## Related Concepts
- [[ft_strcat]] - Full string concatenation
- [[ft_strlcat]] - Safe string concatenation with size limit
- [[ft_strncmp]] - Bounded string comparison
- String Handling - Memory as byte arrays

## Propedeuticity
Builds directly on [[ft_strcat]]. Precedes [[ft_strlcat]] which adds safety guarantees.
