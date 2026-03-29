---
tags: [C03]
---


# ft_strlcat

## What it does
Appends up to `size - strlen(dest) - 1` characters from `src` to `dest`, guaranteeing null termination (if `size > 0`). Returns the total length of the string it tried to create (strlen(src) + strlen(dest)).

## Insight
Unlike strncat, strlcat always null-terminates and returns the theoretical total length, making it safer for buffer management.

## Algorithm
1. Compute `len_dest` = length of `dest`.
2. If `size <= len_dest`, return `size + strlen(src)`.
3. Initialize `i = len_dest`, `j = 0`.
4. While `i < size - 1` and `src[j] != '\0'`, set `dest[i] = src[j]`, increment both.
5. Set `dest[i] = '\0'`.
6. Return `len_dest + strlen(src)`.

## Code (with pedagogical comments)
```c
unsigned int ft_strlcat(char *dest, char *src, unsigned int size)  // Function: concatenates src to dest, returns total length attempted
{
    unsigned int i;  // Index for iterating through dest
    unsigned int j;  // Index for iterating through src
    unsigned int len_dest;  // Stores length of dest
    unsigned int len_src;  // Stores length of src

    len_dest = 0;  // Start counting dest length from 0
    while (dest[len_dest] != '\0')  // Loop until we hit the null terminator
        len_dest++;  // Count each character
    len_src = 0;  // Start counting src length from 0
    while (src[len_src] != '\0')  // Loop until we hit the null terminator
        len_src++;  // Count each character
    if (size <= len_dest)  // If size is <= dest length, truncation will occur
        return (size + len_src);  // Return theoretical total length
    i = len_dest;  // Start appending at end of existing dest content
    j = 0;  // Start copying from beginning of src
    while (src[j] != '\0' && i < size - 1)  // Copy until null or dest is full
    {
        dest[i] = src[j];  // Copy one character from src to dest
        i++;  // Move forward in dest
        j++;  // Move forward in src
    }
    dest[i] = '\0';  // Always null-terminate (if size > 0)
    return (len_dest + len_src);  // Return what the total length WOULD be
}
```

## Line-by-Line Translation
1. `unsigned int ft_strlcat(char *dest, char *src, unsigned int size)` - Define a function that safely concatenates `src` onto `dest` with `size` limit, returning the theoretical total length
2. `unsigned int i; unsigned int j; unsigned int len_dest; unsigned int len_src;` - Declare four unsigned integers: loop counters for dest and src, and variables to store each string's length
3. `len_dest = 0;` - Initialize dest length counter to 0
4. `while (dest[len_dest] != '\0')` - Keep looping as long as we haven't reached the null terminator
5. `len_dest++;` - Increment the length counter for each character found
6. `len_src = 0;` - Initialize src length counter to 0
7. `while (src[len_src] != '\0')` - Count src characters until null terminator
8. `len_src++;` - Increment src length counter for each character
9. `if (size <= len_dest)` - Check if there's no room to append (dest is already >= size)
10. `return (size + len_src);` - Return theoretical length without actually copying
11. `i = len_dest;` - Start appending position at the current end of dest
12. `j = 0;` - Start copying from the beginning of src
13. `while (src[j] != '\0' && i < size - 1)` - Keep copying while src has content AND dest has room (leave space for null terminator)
14. `dest[i] = src[j];` - Copy one character from src to dest
15. `i++; j++;` - Advance both indices
16. `dest[i] = '\0';` - Always null-terminate the result
17. `return (len_dest + len_src);` - Return original dest length + src length (the length of what we tried to create)

## Common Traps
- ❌ Forgetting to null-terminate the result.
- ❌ Not handling `size <= len_dest` case (truncation scenario).
- ❌ Returning wrong value (should be `len_dest + len_src`, not just `len_dest`).

## Related Concepts
- [[ft_strncat]] - Bounded concatenation without safety guarantees
- [[ft_strlcpy]] - Safe string copy
- [[ft_strlen]] - String length calculation
- String Handling - Memory as byte arrays

## Propedeuticity
The "safe" version of string concatenation. Combines concepts from [[ft_strcat]], [[ft_strncat]], and [[ft_strlen]]. Essential for understanding buffer overflow prevention.
