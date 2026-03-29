---
tags: [C03]
---


# ft_strstr

## What it does
Finds the first occurrence of the substring `needle` in the string `haystack`. Returns a pointer to the beginning of the found substring, or NULL if not found.

## Insight
Scan through haystack, at each position check if needle matches starting from that position.

## Algorithm
1. If `needle[0] == '\0'`, return `haystack`.
2. Initialize `i = 0`.
3. While `haystack[i] != '\0'`:
   - Initialize `j = 0`.
   - While `needle[j] != '\0'` and `haystack[i + j] == needle[j]`, increment `j`.
   - If `needle[j] == '\0'`, return `haystack + i`.
   - Increment `i`.
4. Return NULL.

## Code (with pedagogical comments)
```c
char *ft_strstr(char *haystack, char *needle)  // Function: finds first occurrence of needle in haystack
{
    int i;  // Index for iterating through haystack
    int j;  // Index for comparing characters in needle

    if (needle[0] == '\0')  // Special case: empty needle means "found" immediately
        return (haystack);  // Return haystack (empty string found at start)
    i = 0;  // Start at the beginning of haystack
    while (haystack[i] != '\0')  // Loop through each character of haystack
    {
        j = 0;  // Reset needle index to start comparing from needle's beginning
        while (needle[j] != '\0' && haystack[i + j] == needle[j])  // Compare needle chars with haystack at position i
            j++;  // Move to next character in needle while matches continue
        if (needle[j] == '\0')  // If we reached end of needle, all characters matched!
            return (haystack + i);  // Return pointer to where needle was found
        i++;  // Move to next position in haystack to try again
    }
    return (NULL);  // Exhausted haystack without finding needle
}
```

## Line-by-Line Translation
1. `char *ft_strstr(char *haystack, char *needle)` - Define a function that searches for `needle` inside `haystack`, returning a pointer to the match or NULL
2. `int i; int j;` - Declare two integer counters: `i` tracks position in haystack, `j` tracks position in needle
3. `if (needle[0] == '\0')` - Check if needle is an empty string (edge case)
4. `return (haystack);` - An empty needle is "found" at the very beginning of haystack
5. `i = 0;` - Start searching from the first character of haystack
6. `while (haystack[i] != '\0')` - Continue until we've checked every character in haystack
7. `j = 0;` - For each haystack position, reset j to start comparing from needle's beginning
8. `while (needle[j] != '\0' && haystack[i + j] == needle[j])` - Compare consecutive characters: keep going while needle has content AND the characters match
9. `j++;` - Advance to the next character in needle for comparison
10. `if (needle[j] == '\0')` - If we reached the end of needle, every character matched
11. `return (haystack + i);` - Return pointer to the beginning of the matched substring
12. `i++;` - No match at this position, try the next position in haystack
13. `return (NULL);` - Searched entire haystack without finding needle

## Common Traps
- ❌ Not handling empty needle (should return haystack immediately).
- ❌ Returning `&haystack[i]` instead of `haystack + i`.
- ❌ Not checking `needle[j] == '\0'` to confirm full match.

## Related Concepts
- [[ft_strcmp]] - String comparison used within the search
- [[ft_strncmp]] - Bounded comparison
- [[ft_strrchr]] - Find last occurrence of character
- String Handling - Memory as byte arrays

## Propedeuticity
First exercise combining nested loops with string searching. Requires mastery of [[ft_strcmp]] and pointer arithmetic.
