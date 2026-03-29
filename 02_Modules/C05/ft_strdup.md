---
tags: [C05]
---


# ft_strdup

## What it does
Creates a duplicate of the string `s` by allocating memory with `malloc` and copying the string (including the null terminator). Returns a pointer to the new string, or NULL if allocation fails.

## The Insight
First calculate the length of `s`, then allocate `len + 1` bytes, then copy the string. Standard `malloc` + `strcpy` pattern.

## Step-by-step Algorithm
1. Calculate length of `s` by iterating until `\0`.
2. Allocate `len + 1` bytes with `malloc`.
3. If allocation fails, return NULL.
4. Copy each character from `s` to the new buffer, including `\0`.
5. Return the new string.

## The Code (with pedagogical comments)
```c
 <unistd.h>
 <stdlib.h>  // Required for malloc and free

char *ft_strdup(const char *s)  // Function: duplicates string s, returns pointer to new string
{
    char *dup;  // Pointer for the new duplicated string
    int i;  // Counter for copying characters
    int len;  // Variable to store length of original string

    len = 0;  // Start counting length from 0
    while (s[len] != '\0')  // Loop until we reach the null terminator
        len++;  // Count each character
    dup = (char *)malloc(len + 1);  // Allocate memory: len + 1 bytes (extra for '\0')
    if (dup == NULL)  // Check if malloc failed (not enough memory)
        return (NULL);  // Return NULL to indicate allocation failure
    i = 0;  // Start copying from position 0
    while (i <= len)  // Copy all characters INCLUDING the null terminator (that's why <=)
    {
        dup[i] = s[i];  // Copy each character from original to new string
        i++;  // Move to next position
    }
    return (dup);  // Return pointer to the newly allocated duplicated string
}
```

## Line-by-Line Translation
1. `#include <stdlib.h>` - Include standard library header for `malloc` (memory allocation function)
2. `char *ft_strdup(const char *s)` - Define a function that creates a copy of string `s`, returning a pointer to the new string
3. `char *dup; int i; int len;` - Declare: `dup` will point to the new string, `i` is a counter for copying, `len` stores the original string's length
4. `len = 0;` - Initialize length counter to 0
5. `while (s[len] != '\0')` - Loop through each character of `s` until we hit the null terminator
6. `len++;` - Increment len for each character found
7. `dup = (char *)malloc(len + 1);` - Request `len + 1` bytes from heap memory (extra byte for the null terminator)
8. `if (dup == NULL)` - Check if malloc could not allocate memory (system is low on memory)
9. `return (NULL);` - If allocation failed, return NULL to signal error
10. `i = 0;` - Reset counter to 0 to start copying from the beginning
11. `while (i <= len)` - Copy all characters AND the null terminator (using `<=` instead of `<` to include the '\0')
12. `dup[i] = s[i];` - Copy each character one by one from source to destination
13. `i++;` - Advance to next position
14. `return (dup);` - Return the pointer to the newly created duplicate string

## Common Traps
- ❌ Forgetting to include `stdlib.h` for `malloc`.
- ❌ Not checking `malloc` return for NULL.
- ❌ Allocating only `len` bytes instead of `len + 1` (missing null terminator).
- ❌ Using `i < len` instead of `i <= len` in copy loop (would miss null terminator).

---

**Related:** [[ft_strcpy]] [[ft_strncpy]] [[ft_strlcpy]]
