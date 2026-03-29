---
tags: [C05]
---


# ft_strchr

## What it does
Returns a pointer to the first occurrence of character `c` in the string `s`, or NULL if not found. The terminating null byte is considered part of the string, so if `c == '\0'`, it returns a pointer to the terminator.

## The Insight
Iterate through the string until `c` is found. The null terminator is a valid character to search for.

## Step-by-step Algorithm
1. Initialize index `i` to 0.
2. While `s[i] != '\0'`, check if `s[i] == (char)c`. If yes, return `s + i`.
3. Increment `i`.
4. If `c == '\0'`, return `s + i` (pointer to terminator).
5. Return NULL if loop ends without finding.

## The Code (with pedagogical comments)
```c
 <unistd.h>

char *ft_strchr(const char *s, int c)  // Function: finds FIRST occurrence of c in string s
{
    int i;  // Counter for iterating through the string

    i = 0;  // Start from position 0
    while (s[i] != '\0')  // Loop until we reach the null terminator
    {
        if (s[i] == (char)c)  // Check if current character matches target c
            return ((char *)s + i);  // Found! Return pointer to this position
        i++;  // Move to next character
    }
    if (c == '\0')  // Special case: searching for null terminator itself
        return ((char *)s + i);  // Return pointer to the null terminator (end of string)
    return (NULL);  // Searched entire string without finding c
}
```

## Line-by-Line Translation
1. `char *ft_strchr(const char *s, int c)` - Define a function that finds the FIRST occurrence of character `c` in string `s`, returning a pointer or NULL
2. `int i;` - Declare an integer counter `i` to track position in the string
3. `i = 0;` - Start searching from the first character (index 0)
4. `while (s[i] != '\0')` - Continue looping as long as we haven't reached the end of the string
5. `if (s[i] == (char)c)` - Check if the character at position `i` equals our target character `c`
6. `return ((char *)s + i);` - Match found! Return a pointer to that position (cast to char* for return type)
7. `i++;` - No match at this position, advance to the next character
8. `if (c == '\0')` - After the loop, check if we were searching for the null terminator itself
9. `return ((char *)s + i);` - c was '\0', so return pointer to where the null terminator is (end of string)
10. `return (NULL);` - Examined all characters without finding c, return NULL to indicate failure

## Common Traps
- ❌ Forgetting to check for `c == '\0'` case (should return pointer to terminator).
- ❌ Not casting `c` to `char` before comparison.
- ❌ Returning `&s[i]` instead of `s + i`.

---

**Related:** [[ft_strrchr]] [[ft_strnstr]] [[ft_memchr]]
