---
tags: [C06]
---


# ft_range

## What it Does
Allocates and returns an array of integers ranging from `start` to `end` (exclusive).

## The Insight
Calculate the size needed, allocate with `malloc`, then fill the array by iterating from `start` to `end`.

## Step-by-step Algorithm
1. Calculate `size = end - start`.
2. If `size <= 0`, return `NULL`.
3. Allocate `malloc(size * sizeof(int))`.
4. Iterate `i` from 0 to `size - 1`, setting `arr[i] = start + i`.
5. Return `arr`.

## The Code
```c
 <stdlib.h> // Provides malloc() for dynamic memory allocation

// Function: create and return an array of integers from start to end (exclusive)
// Example: ft_range(3, 7) returns [3, 4, 5, 6]
int *ft_range(int start, int end)
{
    int *arr;          // Pointer to the allocated array (to be returned)
    int size;          // Number of integers to allocate
    int i;             // Loop counter for filling the array

    size = end - start;                            // Calculate how many integers we need
    if (size <= 0)                                 // If end <= start, no integers to return
        return (NULL);                             // Return NULL to indicate empty range
    arr = malloc(size * sizeof(int));              // Allocate memory for all integers
    if (!arr)                                      // Check if malloc() failed
        return (NULL);                             // Return NULL to propagate error
    i = 0;                                         // Start filling from index 0
    while (i < size)                               // Loop exactly 'size' times
    {
        arr[i] = start + i;                        // arr[0]=start, arr[1]=start+1, etc.
        i++;                                       // Increment index
    }                                              // Result: [start, start+1, ..., end-1]
    return (arr);                                  // Return the allocated array to the caller
}
```

## Line-by-Line Translation
- `include <stdlib.h>` — Header for malloc() and free() functions
- `int *ft_range(int start, int end)` — Create array of integers in range [start, end)
- `size = end - start;` — Calculate how many integers fit in the range
- `if (size <= 0) return (NULL);` — Handle invalid/empty range (end <= start)
- `arr = malloc(size * sizeof(int));` — Allocate enough bytes for 'size' integers
- `if (!arr) return (NULL);` — Handle malloc failure by returning NULL
- `i = 0;` — Start at the first position in the array
- `while (i < size)` — Fill all positions in the array
- `arr[i] = start + i;` — Store start, start+1, start+2, ... in each position
- `i++;` — Move to the next index
- `return (arr);` — Return the allocated array to the caller

## Related
- ex01 ft_ultimate_range
- ex05 ft_split
