---
tags: [C05]
---


# ft_memchr

## What it does
Scans the first `n` bytes of the memory area for the first occurrence of byte `c`. Returns a pointer to the matching byte, or NULL if not found.

## The Insight
Simple linear search through memory byte-by-byte until `c` is found or `n` bytes are scanned.

## Step-by-step Algorithm
1. Cast `s` to `unsigned char *p`.
2. Initialize index `i` to 0.
3. While `i < n`, check if `p[i] == (unsigned char)c`. If yes, return `p + i`.
4. Increment `i`.
5. Return NULL if loop completes.

## The Code (with pedagogical comments)
```c
 <unistd.h>

void *ft_memchr(const void *s, int c, unsigned int n)  // Find first occurrence of byte c in first n bytes of s
{
    unsigned char *p;  // Pointer to access memory as bytes
    unsigned int i;  // Counter for iteration

    p = (unsigned char *)s;  // Cast void* to unsigned char* for byte-by-byte access
    i = 0;  // Start searching from byte 0
    while (i < n)  // Search through up to n bytes
    {
        if (p[i] == (unsigned char)c)  // If current byte matches target c
            return (p + i);  // Found! Return pointer to this byte position
        i++;  // No match, advance to next byte
    }
    return (NULL);  // Searched n bytes without finding c
}
```

## Line-by-Line Translation
1. `void *ft_memchr(const void *s, int c, unsigned int n)` - Define a function that searches for byte `c` in the first `n` bytes of memory area `s`, returning a pointer to the match or NULL
2. `unsigned char *p; unsigned int i;` - Declare: `p` as a byte pointer to access memory, `i` as a counter for position
3. `p = (unsigned char *)s;` - Cast the generic `void*` pointer to `unsigned char*` so we can read individual bytes
4. `i = 0;` - Start searching from the first byte (offset 0)
5. `while (i < n)` - Continue searching while we're still within the specified `n` bytes
6. `if (p[i] == (unsigned char)c)` - Check if the byte at position `i` equals our target byte `c` (cast to unsigned char ensures proper comparison)
7. `return (p + i);` - Match found! Return a pointer to position `i` in the memory area
8. `i++;` - No match at this position, move to the next byte
9. `return (NULL);` - Searched through all `n` bytes without finding `c`, return NULL

## Common Traps
- ❌ Forgetting to cast `c` to `unsigned char`.
- ❌ Returning `&p[i]` instead of `p + i` (both work, but `p + i` is clearer).
- ❌ Not handling `n == 0` (should return NULL).

---

**Related:** [[ft_memcmp]] [[ft_strchr]]
