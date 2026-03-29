---
tags: [C05]
---


# ft_strrchr

## What it does
Returns a pointer to the last occurrence of character `c` in the string `s`, or NULL if not found. The terminating null byte is considered part of the string.

## The Insight
Scan the entire string to find the last occurrence. Start from the end and work backwards, or scan forward keeping track of the last match.

## Step-by-step Algorithm
1. Initialize index `i` to 0 and a result pointer to NULL.
2. While `s[i] != '\0'`, check if `s[i] == (char)c` and update result pointer.
3. After the loop, check if `c == '\0'` and return pointer to terminator.
4. Return the stored result pointer.

## The Code (with pedagogical comments)
```c
 <unistd.h>

char *ft_strrchr(const char *s, int c)  // Function: finds LAST occurrence of c in string s
{
    char *last;  // Pointer to store the most recent match found
    int i;  // Counter for iterating through string

    last = NULL;  // Initialize to NULL (no match found yet)
    i = 0;  // Start from the beginning of the string
    while (s[i] != '\0')  // Loop through entire string
    {
        if (s[i] == (char)c)  // If current character matches c
            last = (char *)s + i;  // Update last to current position (this way we keep the LAST match)
        i++;  // Move to next character
    }
    if (c == '\0')  // Special case: searching for null terminator
        return ((char *)s + i);  // Return pointer to the null terminator at end of string
    return (last);  // Return pointer to last occurrence, or NULL if not found
}
```

## Line-by-Line Translation
1. `char *ft_strrchr(const char *s, int c)` - Define a function that finds the LAST occurrence of character `c` in string `s`, returning a pointer or NULL
2. `char *last; int i;` - Declare: `last` will store the most recent match position, `i` iterates through the string
3. `last = NULL;` - Start with no match found (NULL means not found yet)
4. `i = 0;` - Begin iteration from the first character
5. `while (s[i] != '\0')` - Continue until we've examined every character in the string
6. `if (s[i] == (char)c)` - Check if current character matches the target character `c`
7. `last = (char *)s + i;` - Update `last` to current position (this replaces any previous match, so after the loop, `last` points to the LAST occurrence)
8. `i++;` - Move to the next character position
9. `if (c == '\0')` - Special case: if searching for the null terminator itself
10. `return ((char *)s + i);` - Return pointer to the null terminator at position `i` (which is past the last character)
11. `return (last);` - Return pointer to the last occurrence of `c`, or NULL if we never updated `last`

## Common Traps
- ❌ Forgetting to track the last occurrence (only returning first).
- ❌ Not handling `c == '\0'` correctly (should return pointer to terminator).
- ❌ Returning NULL when `c == '\0'` is found at end.

---

**Related:** [[ft_strchr]] [[ft_strnstr]]
