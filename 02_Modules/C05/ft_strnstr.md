---
tags: [C05]
---


# ft_strnstr

## What it does
Locates the first occurrence of the null-terminated string `needle` in the string `haystack`, where not more than `len` characters are searched. Returns a pointer to the beginning of the found substring, or NULL if not found.

## The Insight
For each position in `haystack` (up to `len`), check if `needle` matches. Only match if there's enough room for `needle` to fit within `len`.

## Step-by-step Algorithm
1. If `needle[0] == '\0'`, return `haystack`.
2. Initialize index `i` to 0.
3. While `i < len` and `haystack[i] != '\0'`, try matching `needle` starting at `haystack[i]`.
4. For each match attempt, check if all characters of `needle` match and `i + needle_len <= len`.
5. If match found, return `haystack + i`.
6. Increment `i`.
7. Return NULL if no match found.

## The Code (with pedagogical comments)
```c
 <unistd.h>

char *ft_strnstr(const char *haystack, const char *needle, unsigned int len)  // Find needle in haystack within len bytes
{
    unsigned int i;  // Index for iterating through haystack
    unsigned int j;  // Index for comparing characters in needle
    unsigned int needle_len;  // Length of needle string

    if (needle[0] == '\0')  // Edge case: empty needle is "found" immediately
        return ((char *)haystack);  // Return haystack pointer (empty string at start)
    needle_len = 0;  // Calculate needle's length first
    while (needle[needle_len] != '\0')  // Loop until end of needle
        needle_len++;  // Count each character
    i = 0;  // Start searching from beginning of haystack
    while (haystack[i] != '\0' && i < len)  // Search while haystack has chars AND we're within len limit
    {
        j = 0;  // Reset to start of needle for each new position in haystack
        while (haystack[i + j] == needle[j] && i + j < len)  // Compare chars while they match AND within bounds
        {
            j++;  // Move to next character in needle
            if (j == needle_len)  // If we've matched all characters of needle
                return ((char *)haystack + i);  // Return pointer to match position in haystack
        }
        i++;  // No match at this position, try next position in haystack
    }
    return (NULL);  // Searched within len bytes without finding needle
}
```

## Line-by-Line Translation
1. `char *ft_strnstr(const char *haystack, const char *needle, unsigned int len)` - Define a function that locates `needle` inside `haystack`, searching at most `len` bytes, returning pointer to match or NULL
2. `unsigned int i; unsigned int j; unsigned int needle_len;` - Declare: `i` tracks position in haystack, `j` tracks position in needle, `needle_len` stores needle's length
3. `if (needle[0] == '\0')` - Check if needle is an empty string (edge case)
4. `return ((char *)haystack);` - Empty needle is considered "found" at position 0 of haystack
5. `needle_len = 0;` - Calculate needle length first (we need it to detect full match)
6. `while (needle[needle_len] != '\0')` - Count characters until null terminator
7. `needle_len++;` - Increment counter for each character
8. `i = 0;` - Start searching from haystack's beginning
9. `while (haystack[i] != '\0' && i < len)` - Loop while haystack has characters AND we haven't exceeded search limit
10. `j = 0;` - For each haystack position, reset to start comparing needle from its beginning
11. `while (haystack[i + j] == needle[j] && i + j < len)` - Compare chars: keep going while they match AND we stay within the len limit
12. `j++;` - Advance to next character in needle
13. `if (j == needle_len)` - Check if we've matched all characters of needle
14. `return ((char *)haystack + i);` - Complete match found, return pointer to position i in haystack
15. `i++;` - No match at current position, try next position in haystack
16. `return (NULL);` - Searched through len bytes without finding needle

## Common Traps
- ❌ Forgetting to handle `needle == ""` (empty string returns haystack).
- ❌ Not checking `i + j < len` to stay within bounds.
- ❌ Not computing `needle_len` first.

---

**Related:** [[ft_strchr]] [[ft_strrchr]] [[ft_strdup]]
