---
tags: [C05]
---


# ft_memcpy

## What it does
Copies `n` bytes from memory area `src` to memory area `dest`. The areas must not overlap. Returns a pointer to `dest`.

## The Insight
Simple memory copy byte-by-byte. Unlike `memmove`, this does not handle overlapping memory safely. Cast both pointers to `unsigned char *`.

## Step-by-step Algorithm
1. Cast `dest` to `unsigned char *d` and `src` to `unsigned char *s`.
2. Initialize index `i` to 0.
3. While `i < n`, set `d[i] = s[i]` and increment `i`.
4. Return `dest`.

## The Code (with pedagogical comments)
```c
 <unistd.h>

void *ft_memcpy(void *dest, const void *src, unsigned int n)  // Copy n bytes from src to dest (no overlap handling)
{
    unsigned char *d;  // Pointer to dest memory area (as bytes)
    unsigned char *s;  // Pointer to src memory area (as bytes)
    unsigned int i;  // Counter for iteration

    d = (unsigned char *)dest;  // Cast dest to byte pointer for byte-by-byte access
    s = (unsigned char *)src;  // Cast src to byte pointer for byte-by-byte reading
    i = 0;  // Start copying from byte 0
    while (i < n)  // Copy n bytes total
    {
        d[i] = s[i];  // Copy one byte from src to dest at position i
        i++;  // Advance to next byte
    }
    return (dest);  // Return dest pointer (conventional return for memory functions)
}
```

## Line-by-Line Translation
1. `void *ft_memcpy(void *dest, const void *src, unsigned int n)` - Define a function that copies exactly `n` bytes from `src` to `dest`, returning `dest` (does NOT handle overlapping memory - use memmove for that)
2. `unsigned char *d; unsigned char *s; unsigned int i;` - Declare: `d` and `s` as byte pointers for dest and src, `i` as a loop counter
3. `d = (unsigned char *)dest;` - Cast the generic `dest` pointer to `unsigned char*` so we can access individual bytes
4. `s = (unsigned char *)src;` - Cast the generic `src` pointer to `unsigned char*` so we can read individual bytes
5. `i = 0;` - Initialize counter to 0, starting from the first byte
6. `while (i < n)` - Loop to copy exactly n bytes
7. `d[i] = s[i];` - Copy one byte from src to dest at the current position i
8. `i++;` - Increment i to advance to the next byte position
9. `return (dest);` - Return the destination pointer (standard convention for memory functions)

## Common Traps
- ❌ Not handling overlapping memory (use `memmove` for that).
- ❌ Forgetting to cast to `unsigned char *`.
- ❌ Not returning `dest`.

---

**Related:** [[ft_memmove]] [[ft_memccpy]] [[ft_bzero]]
