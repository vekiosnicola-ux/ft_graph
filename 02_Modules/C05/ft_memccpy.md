---
tags: [C05]
---


# ft_memccpy

## What it does
Copies bytes from `src` to `dest` up to `n` bytes, stopping when character `c` is found. Returns a pointer to the byte after the copy of `c` in `dest`, or NULL if `c` was not found in `n` bytes.

## The Insight
The "stop byte" feature requires checking each copied byte for `c`. If found, copy it too and return immediately.

## Step-by-step Algorithm
1. Cast `dest` to `unsigned char *d` and `src` to `unsigned char *s`.
2. Initialize index `i` to 0.
3. While `i < n`, set `d[i] = s[i]`.
4. If `d[i] == (unsigned char)c`, return `d + i + 1`.
5. Increment `i`.
6. Return NULL if `c` not found within `n` bytes.

## The Code (with pedagogical comments)
```c
 <unistd.h>

void *ft_memccpy(void *dest, const void *src, int c, unsigned int n)  // Copy from src to dest, stop when c is copied
{
    unsigned char *d;  // Pointer to dest memory area (as bytes)
    unsigned char *s;  // Pointer to src memory area (as bytes)
    unsigned int i;  // Counter for iteration

    d = (unsigned char *)dest;  // Cast dest to byte pointer
    s = (unsigned char *)src;  // Cast src to byte pointer
    i = 0;  // Start copying from position 0
    while (i < n)  // Copy up to n bytes
    {
        d[i] = s[i];  // Copy one byte from src to dest
        if (d[i] == (unsigned char)c)  // Check if we just copied the stop byte c
            return (d + i + 1);  // Return pointer to byte AFTER the copied c
        i++;  // Not c, continue to next byte
    }
    return (NULL);  // Copied n bytes without finding c
}
```

## Line-by-Line Translation
1. `void *ft_memccpy(void *dest, const void *src, int c, unsigned int n)` - Define a function that copies bytes from `src` to `dest` until byte `c` is copied (or n bytes copied), returning pointer to byte after c, or NULL
2. `unsigned char *d; unsigned char *s; unsigned int i;` - Declare: `d` and `s` as byte pointers for dest and src, `i` as a counter
3. `d = (unsigned char *)dest;` - Cast dest from void* to unsigned char* for byte access
4. `s = (unsigned char *)src;` - Cast src from void* to unsigned char* for byte access
5. `i = 0;` - Start copying from the first byte (offset 0)
6. `while (i < n)` - Continue copying while we haven't exceeded n bytes
7. `d[i] = s[i];` - Copy one byte from src to dest at position i
8. `if (d[i] == (unsigned char)c)` - Check if the byte we just copied equals the stop byte `c`
9. `return (d + i + 1);` - Found c! Return pointer to the position AFTER where c was copied (c is at d[i], so d+i+1 is right after it)
10. `i++;` - The byte wasn't c, advance to copy the next byte
11. `return (NULL);` - Copied n bytes without encountering c, return NULL

## Common Traps
- ❌ Forgetting to copy `c` before returning.
- ❌ Returning `d + i` instead of `d + i + 1` (pointer should be AFTER the copied c).
- ❌ Not casting `c` to `unsigned char` before comparison.

---

**Related:** [[ft_memcpy]] [[ft_memmove]]
