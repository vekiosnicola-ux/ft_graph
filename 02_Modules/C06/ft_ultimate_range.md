---
tags: [C06]
---


# ft_ultimate_range

## What it Does
Allocates and fills an array of integers from `start` to `end` (exclusive), and stores its size in `*range`.

## The Insight
Similar to `ft_range` but stores the array size in a pointer parameter. Returns -1 on failure, 0 on success.

## Step-by-step Algorithm
1. Calculate `size = end - start`.
2. If `size <= 0`, set `*range = 0` and return -1.
3. Allocate `malloc(size * sizeof(int))`.
4. If allocation fails, set `*range = 0` and return -1.
5. Fill `arr[i] = start + i`.
6. Set `*range = size`.
7. Return 0.

## The Code
```c
 <stdlib.h> // Provides malloc() for dynamic memory allocation

// Function: create an array of integers from start to end (exclusive)
// Stores the array pointer in *range and returns the size, or -1 on failure
int ft_ultimate_range(int **range, int start, int end)
{
    int *arr;          // Pointer to the allocated array of integers
    int size;          // Number of integers in the range (end - start)
    int i;             // Loop counter for filling the array

    size = end - start;                            // Calculate how many integers we need
    if (size <= 0)                                // If range is empty or invalid
    {
        *range = 0;                                // Set caller's pointer to NULL
        return (0);                                // Return 0 to indicate empty range
    }                                              // (Note: returns 0, not -1, for empty)
    arr = malloc(size * sizeof(int));              // Allocate memory for 'size' integers
    if (!arr)                                      // Check for malloc failure
    {
        *range = 0;                                // Set caller's pointer to NULL
        return (-1);                               // Return -1 to indicate error
    }
    i = 0;                                         // Start filling from index 0
    while (i < size)                              // Fill the array with values
    {
        arr[i] = start + i;                        // arr[i] = start, start+1, start+2, ...
        i++;                                       // Move to next index
    }                                              // Result: [start, start+1, ..., end-1]
    *range = arr;                                  // Pass the array back to the caller
    return (size);                                 // Return the number of integers
}
```

## Line-by-Line Translation
- `include <stdlib.h>` — Header for malloc() and free()
- `int ft_ultimate_range(int **range, int start, int end)` — Create range, store in *range
- `size = end - start;` — Calculate how many integers fit in [start, end)
- `if (size <= 0)` — Handle empty or invalid range
- `*range = 0;` — Set caller's pointer to NULL (0 is NULL)
- `return (0);` — Return 0 for empty range
- `arr = malloc(size * sizeof(int));` — Allocate memory for all integers
- `if (!arr)` — Check if malloc failed
- `*range = 0; return (-1);` — Set pointer to NULL and return error code
- `i = 0; while (i < size)` — Loop to fill the array
- `arr[i] = start + i;` — Store each integer in sequence
- `*range = arr;` — Pass array pointer back to caller via pointer-to-pointer
- `return (size);` — Return the number of integers in the range

## Related
- ex00 ft_range
