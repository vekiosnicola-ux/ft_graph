---
tags: [C05]
---


# ft_memset

## What it does
Fills the first `n` bytes of the memory area pointed to by `b` with the constant byte `c`. Returns a pointer to the memory area `b`.

## The Insight
This is a simple memory-fill operation. Cast the pointer to `unsigned char *` to handle byte-by-byte filling correctly, avoiding issues with type aliasing.

## Step-by-step Algorithm
1. Cast `b` to `unsigned char *p`.
2. Initialize index `i` to 0.
3. While `i < n`, set `p[i] = (unsigned char)c` and increment `i`.
4. Return `b`.

## The Code (with pedagogical comments)
```c
 <unistd.h>

void *ft_memset(void *b, int c, unsigned int n)  // Fill first n bytes of memory b with byte c
{
    unsigned char *p;  // Pointer to memory area (cast to byte pointer)
    unsigned int i;  // Counter for iteration

    p = (unsigned char *)b;  // Cast void* to unsigned char* for byte-by-byte access
    i = 0;  // Start filling from byte 0
    while (i < n)  // Fill n bytes total
    {
        p[i] = (unsigned char)c;  // Set byte at position i to the value c (cast to byte)
        i++;  // Move to next byte
    }
    return (b);  // Return the original pointer b (conventional return)
}
```

## Line-by-Line Translation
1. `void *ft_memset(void *b, int c, unsigned int n)` - Define a function that fills the first `n` bytes of memory area `b` with the byte value `c`, returning `b`
2. `unsigned char *p; unsigned int i;` - Declare: `p` as a byte pointer to access memory, `i` as a loop counter
3. `p = (unsigned char *)b;` - Cast the generic `void*` pointer to `unsigned char*` so we can write to individual bytes
4. `i = 0;` - Start filling from the first byte (offset 0)
5. `while (i < n)` - Continue filling while we haven't set n bytes
6. `p[i] = (unsigned char)c;` - Write the byte value `c` to position i (casting to unsigned char ensures proper byte-sized write)
7. `i++;` - Advance to the next byte position
8. `return (b);` - Return the original memory pointer `b` (standard convention for memory functions)

## Common Traps
- ❌ Not casting to `unsigned char *` (undefined behavior for non-byte values).
- ❌ Using `int` for index when `n` is `unsigned int`.
- ❌ Forgetting to return `b`.

---

**Related:** [[ft_bzero]] [[ft_memcpy]] [[ft_memmove]]
