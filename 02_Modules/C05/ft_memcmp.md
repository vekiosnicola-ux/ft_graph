---
tags: [C05]
---


# ft_memcmp

## What it does
Compares the first `n` bytes of memory areas `s1` and `s2`. Returns an integer less than, equal to, or greater than zero if `s1` is found to be less than, to match, or be greater than `s2`.

## The Insight
Compares byte-by-byte until a difference is found or all `n` bytes match. The difference is returned as `s1[i] - s2[i]`.

## Step-by-step Algorithm
1. Cast both to `unsigned char *`.
2. Initialize index `i` to 0.
3. While `i < n`, compare `s1[i]` and `s2[i]`.
4. If they differ, return `s1[i] - s2[i]`.
5. Increment `i`.
6. Return 0 if all bytes match.

## The Code (with pedagogical comments)
```c
 <unistd.h>

int ft_memcmp(const void *s1, const void *s2, unsigned int n)  // Compare first n bytes of two memory areas
{
    unsigned char *p1;  // Pointer to first memory area (cast to byte access)
    unsigned char *p2;  // Pointer to second memory area (cast to byte access)
    unsigned int i;  // Counter for iteration

    p1 = (unsigned char *)s1;  // Cast void* to unsigned char* for byte-by-byte access
    p2 = (unsigned char *)s2;  // Cast void* to unsigned char* for byte-by-byte access
    i = 0;  // Start comparing from byte 0
    while (i < n)  // Compare up to n bytes
    {
        if (p1[i] != p2[i])  // If bytes differ at position i
            return (p1[i] - p2[i]);  // Return the difference (sign indicates which is greater)
        i++;  // Bytes matched, move to next position
    }
    return (0);  // All n bytes matched, return 0 (equal)
}
```

## Line-by-Line Translation
1. `int ft_memcmp(const void *s1, const void *s2, unsigned int n)` - Define a function that compares the first `n` bytes of two memory regions, returning: negative if s1 < s2, 0 if equal, positive if s1 > s2
2. `unsigned char *p1; unsigned char *p2; unsigned int i;` - Declare: `p1` and `p2` as byte pointers to access memory areas, `i` as a counter
3. `p1 = (unsigned char *)s1;` - Cast the generic pointer `s1` to an unsigned char pointer so we can access bytes
4. `p2 = (unsigned char *)s2;` - Cast the generic pointer `s2` to an unsigned char pointer for byte access
5. `i = 0;` - Start comparison from the first byte
6. `while (i < n)` - Continue comparing while we haven't exceeded the n-byte limit
7. `if (p1[i] != p2[i])` - Check if the bytes at position `i` are different
8. `return (p1[i] - p2[i]);` - Return the difference: negative if p1[i] < p2[i], positive if p1[i] > p2[i] (casting to unsigned ensures proper arithmetic)
9. `i++;` - Bytes at position i matched, advance to the next byte
10. `return (0);` - Compared all n bytes without finding a difference, the memory areas are equal

## Common Traps
- ❌ Using `unsigned int` difference directly (may overflow).
- ❌ Forgetting to cast to `unsigned char *`.
- ❌ Not returning difference as `int` (sign matters).

---

**Related:** [[ft_memchr]] [[ft_strcmp]]
