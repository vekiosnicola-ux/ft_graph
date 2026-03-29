---
tags: [C05]
---


# ft_bzero

## What it does
Erases the first `n` bytes of the memory area pointed to by `s` by writing zeros. No return value.

## The Insight
Equivalent to `memset(s, 0, n)`. Cast to `unsigned char *` to write byte-by-byte.

## Step-by-step Algorithm
1. Cast `s` to `unsigned char *p`.
2. Initialize index `i` to 0.
3. While `i < n`, set `p[i] = 0` and increment `i`.
4. Return (void).

## The Code (with pedagogical comments)
```c
 <unistd.h>

void ft_bzero(void *s, unsigned int n)  // Set the first n bytes of memory area s to zero
{
    unsigned char *p;  // Pointer to memory area (cast to byte pointer)
    unsigned int i;  // Counter for iteration

    p = (unsigned char *)s;  // Cast void* to unsigned char* for byte-by-byte writing
    i = 0;  // Start from byte 0
    while (i < n)  // Zero out n bytes
    {
        p[i] = 0;  // Set byte at position i to 0 (null byte)
        i++;  // Move to next byte
    }
}
```

## Line-by-Line Translation
1. `void ft_bzero(void *s, unsigned int n)` - Define a procedure that fills the first `n` bytes of memory area `s` with zeros (no return value)
2. `unsigned char *p; unsigned int i;` - Declare: `p` as a byte pointer to access memory, `i` as a loop counter
3. `p = (unsigned char *)s;` - Cast the generic `void*` pointer to `unsigned char*` so we can write to individual bytes
4. `i = 0;` - Start zeroing from the first byte (offset 0)
5. `while (i < n)` - Continue zeroing while we haven't set n bytes
6. `p[i] = 0;` - Set the byte at position i to 0 (ASCII null character)
7. `i++;` - Advance to the next byte position
8. (no return statement) - `bzero` is a void function, it doesn't return anything

## Common Traps
- ❌ Not casting to `unsigned char *`.
- ❌ Confusing `n` as element count vs byte count (it's bytes).
- ❌ Forgetting this function has no return value.

---

**Related:** [[ft_memset]] [[ft_memcpy]]
