---
tags: [C06]
---


# ft_strtrim

## What it Does
Returns a copy of the string with leading and trailing characters from `set` removed.

## The Insight
Find the first and last characters not in `set`, then substring the trimmed portion.

## Step-by-step Algorithm
1. If `s1` or `set` is NULL, return NULL.
2. Find `start` by incrementing while `s1[start]` is in `set`.
3. Find `end` by decrementing while `s1[end]` is in `set`.
4. If `start > end`, return `malloc(1)` with '\0'.
5. Allocate `malloc(end - start + 2)`.
6. Copy characters from `start` to `end` inclusive.
7. Null-terminate and return.

## The Code
```c
 <stdlib.h> // Provides malloc() for dynamic memory allocation

// Helper function: checks if character c exists in the string 'set'
int ft_is_in_set(char c, char *set)
{
    int i;              // Loop counter to iterate through set

    i = 0;              // Start at the first character of set
    while (set[i])      // Loop until we hit the null terminator '\0'
    {
        if (c == set[i]) // Does c match this character in set?
            return (1);   // Yes: c is in the set
        i++;              // No: check the next character in set
    }
    return (0);         // c was not found in set
}

// Main function: trim leading and trailing characters from set
char *ft_strtrim(char const *s1, char const *set)
{
    char *result;       // Pointer to the trimmed string (will be returned)
    int start;          // Index of first character NOT in set (from left)
    int end;            // Index of first character NOT in set (from right)
    int i;              // Loop counter for copying characters

    if (!s1 || !set)    // Guard: check for NULL pointers
        return (NULL);  // Cannot trim NULL strings
    start = 0;          // Start from the beginning of s1
    while (s1[start] && ft_is_in_set(s1[start], (char *)set))  // Skip leading chars in set
        start++;        // Move start forward until we find a character not in set
    end = 0;            // Initialize end to 0 first
    while (s1[end])     // Find the length of s1 by incrementing end
        end++;          // end will be the index of the null terminator '\0'
    while (end > start && ft_is_in_set(s1[end - 1], (char *)set))  // Trim trailing
        end--;          // Move end backward while last chars are in set
    if (start >= end)   // Edge case: entire string was trimmed away
        return (malloc(1));  // Return an empty string (just '\0')
    result = malloc(end - start + 1);  // Allocate memory for trimmed portion
    if (!result)        // Check for malloc failure
        return (NULL);  // Propagate error
    i = 0;              // Copy characters from s1 to result
    while (start < end) // Copy exactly (end - start) characters
        result[i++] = s1[start++];  // Copy and move both pointers
    result[i] = '\0';   // Null-terminate the result string
    return (result);    // Return the trimmed string
}
```

## Line-by-Line Translation
- `include <stdlib.h>` — Header for malloc() and free()
- `int ft_is_in_set(char c, char *set)` — Check if character c is in the set string
- `while (set[i])` — Loop through all characters in set
- `if (c == set[i]) return (1);` — Found: c is in the set
- `return (0);` — Not found: c is not in the set
- `char *ft_strtrim(char const *s1, char const *set)` — Trim chars from both ends
- `if (!s1 || !set) return (NULL);` — Handle NULL inputs
- `start = 0;` — Start from the beginning
- `while (s1[start] && ft_is_in_set(...))` — Skip leading characters that are in set
- `start++;` — Move forward
- `end = 0; while (s1[end]) end++;` — Find the length of s1 (index of '\0')
- `while (end > start && ft_is_in_set(...))` — Skip trailing characters in set
- `end--;` — Move backward
- `if (start >= end) return (malloc(1));` — All characters were trimmed
- `result = malloc(end - start + 1);` — Allocate exact size needed
- `while (start < end) result[i++] = s1[start++];` — Copy the trimmed portion
- `result[i] = '\0';` — Null-terminate the result
- `return (result);` — Return the trimmed string

## Related
- ex03 ft_strjoin
- ex05 ft_split
