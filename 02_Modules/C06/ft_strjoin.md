---
tags: [C06]
---


# ft_strjoin

## What it Does
Concatenates all strings in `tab` into a single new string, separated by `sep`.

## The Insight
First pass to calculate total length, then allocate and copy each string with separator.

## Step-by-step Algorithm
1. If `tab` is NULL or `tab[0]` is NULL, return `malloc(1)` with '\0'.
2. Count number of strings (`size`) and calculate total length including separators.
3. Allocate `malloc(total_length + 1)`.
4. Copy each string, adding `sep` between (but not after the last).
5. Null-terminate.
6. Return result.

## The Code
```c
 <stdlib.h> // Provides malloc() for dynamic memory allocation

// Main function: concatenate all strings with separator between each
char *ft_strjoin(int size, char **strs, char *sep)
{
    char *result;       // Pointer to the concatenated string (will be returned)
    char *ptr;          // Moving pointer to track where to write next
    int i;              // Loop counter for iterating through strs array
    int j;              // Loop counter for iterating through each string
    int total_len;      // Total length needed for the result string

    if (size == 0)      // Edge case: no strings to join
        return (malloc(1));  // Return an empty string (just the null terminator)
    total_len = 0;      // Start counting total length at 0
    i = 0;              // Start with the first string in the array
    while (i < size)    // Loop through all strings in the array
    {
        j = 0;          // Reset j to start of current string
        while (strs[i][j])  // Count characters in this string
            total_len++, j++;  // Add to total and move to next char
        if (i < size - 1)    // If NOT the last string, add separator length
        {
            j = 0;            // Reset j to start of separator
            while (sep[j])    // Count characters in separator
                total_len++, j++;  // Add separator length to total
        }
        i++;                 // Move to next string in the array
    }                        // total_len now equals all chars + all separators
    result = malloc(total_len + 1);  // Allocate exactly what we need + null terminator
    if (!result)             // Check for malloc failure
        return (NULL);      // Propagate error
    ptr = result;            // ptr tracks current write position in result
    i = 0;                   // Reset i to first string
    while (i < size)        // Copy each string into result
    {
        j = 0;               // Reset j to start of current string
        while (strs[i][j])   // Copy all characters of current string
            *ptr++ = strs[i][j++];  // Copy char and move both pointers forward
        if (i < size - 1)    // If NOT the last string, add separator
        {
            j = 0;            // Reset j to start of separator
            while (sep[j])    // Copy separator characters
                *ptr++ = sep[j++];  // Copy and advance
        }
        i++;                  // Move to next string
    }
    *ptr = '\0';              // Null-terminate the final string
    return (result);          // Return the concatenated string
}
```

## Line-by-Line Translation
- `include <stdlib.h>` — Header for malloc() and free()
- `char *ft_strjoin(int size, char **strs, char *sep)` — Concatenate strings with separator
- `if (size == 0) return (malloc(1));` — Handle empty input case
- `total_len = 0;` — Initialize total length counter
- `while (i < size)` — Loop through all strings
- `while (strs[i][j]) total_len++, j++;` — Count characters in each string
- `if (i < size - 1)` — Only add separator if not the last string
- `while (sep[j]) total_len++, j++;` — Count separator characters
- `result = malloc(total_len + 1);` — Allocate exact memory needed
- `ptr = result;` — Use ptr to track write position
- `while (i < size)` — Second pass: copy strings
- `*ptr++ = strs[i][j++];` — Copy characters using pointer arithmetic
- `*ptr++ = sep[j++];` — Copy separator between strings
- `*ptr = '\0';` — Null-terminate the result
- `return (result);` — Return the concatenated string

## Related
- ex02 ft_concat_params
- ex04 ft_strtrim
