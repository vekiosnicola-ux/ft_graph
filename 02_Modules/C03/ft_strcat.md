---
tags: [C03]
---


# ft_strcat

## What it does
Appends the `src` string to the end of `dest`, overwriting the '\0' at the end of dest and adding a new '\0' at the end. Returns `dest`.

## Insight
Find the end of dest (where '\0' is), then copy src characters starting from that position.

## Algorithm
1. Find the index `i` where `dest[i] == '\0'`.
2. Initialize `j = 0`.
3. While `src[j] != '\0'`, set `dest[i + j] = src[j]` and increment `j`.
4. Set `dest[i + j] = '\0'`.
5. Return `dest`.

## Code (with pedagogical comments)
```c
char *ft_strcat(char *dest, char *src)  // Function: appends entire src string to end of dest
{
    int i;  // Index to find the end of dest
    int j;  // Index to iterate through src

    i = 0;  // Start at position 0 in dest
    while (dest[i] != '\0')  // Loop until we find dest's null terminator (end of dest)
        i++;  // Advance i until dest[i] == '\0'
    j = 0;  // Start copying from beginning of src
    while (src[j] != '\0')  // Loop through entire src until its null terminator
    {
        dest[i + j] = src[j];  // Copy src[j] to the end of dest (dest[i] is '\0', so i+j is right after dest content)
        j++;  // Move to next character in src
    }
    dest[i + j] = '\0';  // Add null terminator to mark end of combined string
    return (dest);  // Return pointer to beginning of dest (same as input)
}
```

## Line-by-Line Translation
1. `char *ft_strcat(char *dest, char *src)` - Define a function that concatenates `src` onto the end of `dest`, returning `dest`
2. `int i; int j;` - Declare two integer variables: `i` will track position in dest, `j` will track position in src
3. `i = 0;` - Start checking dest from index 0
4. `while (dest[i] != '\0')` - Keep advancing `i` while we haven't hit dest's null terminator
5. `i++;` - Move one position forward
6. `j = 0;` - Reset j to 0 to start copying src from its beginning
7. `while (src[j] != '\0')` - Keep copying while src still has characters
8. `dest[i + j] = src[j];` - Place src character at position i+j in dest (i is at end of original dest, j offsets into src)
9. `j++;` - Increment j to get next character from src
10. `dest[i + j] = '\0';` - After copying all of src, append null terminator to properly end the new string
11. `return (dest);` - Return the original dest pointer (convention for string functions)

## Common Traps
- ❌ Not finding the end of dest first (would overwrite dest instead of appending).
- ❌ Forgetting to add '\0' at the end of the combined string.
- ❌ Not returning dest (should return the original pointer).

## Related Concepts
- [[ft_strncat]] - Bounded string concatenation
- [[ft_strlcat]] - Safe string concatenation
- [[ft_strcpy]] - String copy
- String Handling - Memory as byte arrays

## Propedeuticity
Foundation for [[ft_strncat]] and [[ft_strlcat]]. Understanding null-termination is critical for all string exercises.
