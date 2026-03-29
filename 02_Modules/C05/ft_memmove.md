---
tags: [C05]
---


# ft_memmove

## What it does
Copies `n` bytes from memory area `src` to memory area `dest`. Handles overlapping memory correctly. Returns a pointer to `dest`.

## The Insight
The key difference from `memcpy` is handling overlap. If `src` is before `dest` in memory, copy backwards to avoid corrupting data before it's moved.

## Step-by-step Algorithm
1. Cast both to `unsigned char *`.
2. If `dest < src` (no overlap or src before dest), copy forwards.
3. Otherwise, copy backwards starting from the end.
4. Return `dest`.

## The Code (with pedagogical comments)
```c
 <unistd.h>

void *ft_memmove(void *dest, const void *src, unsigned int n)  // Copy n bytes from src to dest, handles overlap
{
    unsigned char *d;  // Pointer to dest memory area (as bytes)
    unsigned char *s;  // Pointer to src memory area (as bytes)
    unsigned int i;  // Counter for iteration

    d = (unsigned char *)dest;  // Cast dest to byte pointer for byte-by-byte copying
    s = (unsigned char *)src;  // Cast src to byte pointer for byte-by-byte reading
    if (dest < src)  // Case 1: dest is BEFORE src in memory (no overlap if copying forward)
    {
        i = 0;  // Start copying from beginning
        while (i < n)  // Copy n bytes
        {
            d[i] = s[i];  // Copy byte from src to dest
            i++;  // Move to next byte
        }
    }
    else if (n > 0)  // Case 2: dest is AT OR AFTER src in memory (potential overlap)
    {
        i = n;  // Start from the END to avoid overwriting src before it's copied
        while (i > 0)  // Copy backwards until we've copied all n bytes
        {
            d[i - 1] = s[i - 1];  // Copy byte from src to dest (working backwards)
            i--;  // Move to previous byte
        }
    }
    return (dest);  // Return dest pointer (conventional return for memory functions)
}
```

## Line-by-Line Translation
1. `void *ft_memmove(void *dest, const void *src, unsigned int n)` - Define a function that copies `n` bytes from `src` to `dest`, safely handling overlapping memory regions, returning `dest`
2. `unsigned char *d; unsigned char *s; unsigned int i;` - Declare: `d` and `s` as byte pointers for dest and src, `i` as a counter
3. `d = (unsigned char *)dest;` - Cast `dest` from `void*` to `unsigned char*` for byte-level access
4. `s = (unsigned char *)src;` - Cast `src` from `void*` to `unsigned char*` for byte-level access
5. `if (dest < src)` - Check if dest address is lower than src address (src comes after dest in memory)
6. `i = 0;` - If copying forward, start from byte 0
7. `while (i < n)` - Copy n bytes total
8. `d[i] = s[i];` - Copy one byte from src to dest at position i
9. `i++;` - Advance to next byte
10. `else if (n > 0)` - If dest is at or after src (overlap possible), and there's actually something to copy
11. `i = n;` - Start from the END (last byte to copy)
12. `while (i > 0)` - Continue until we've copied all n bytes
13. `d[i - 1] = s[i - 1];` - Copy byte at position i-1 (i is now one past the last byte to copy)
14. `i--;` - Move backwards to previous byte
15. `return (dest);` - Return the destination pointer (standard convention for memory functions)

## Common Traps
- ❌ Using `memcpy` logic (doesn't handle overlap correctly).
- ❌ Forgetting to check `dest < src` for direction.
- ❌ Not handling `n == 0` case properly.

---

**Related:** [[ft_memcpy]] [[ft_memccpy]]
