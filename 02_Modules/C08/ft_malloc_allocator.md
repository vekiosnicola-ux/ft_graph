---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# ft_malloc_allocator

---
tags: [C08, magenta]
---

## Navigation
← C08_INDEX|C08 INDEX | [[ft_arrs_swap|Next: ft_arrs_swap →]]

## What it does
Allocates memory for an array of integers and initializes it with values from 0 to `size - 1`.

## The Insight
Uses `malloc` to allocate memory on the heap. Must calculate size as `size * sizeof(int)`.

## Step-by-step Algorithm
1. Allocate memory using `malloc(size * sizeof(int))`.
2. Check if allocation succeeded (not NULL).
3. Initialize each element with its index.
4. Return the pointer.

## The Code
```c
 <stdlib.h>  // Provides malloc() for dynamic memory allocation

int *ft_malloc_allocator(int size)  // Function takes desired array size
{
    int *arr;  // Pointer to hold the base address of allocated array
    int i;     // Loop counter to iterate through array indices

    if (size <= 0)  // Validate: reject invalid sizes (0 or negative)
        return (NULL);  // Return NULL to indicate error
    arr = malloc(size * sizeof(int));  // Request memory: size elements × bytes per int
    if (arr == NULL)  // Check if malloc failed (out of memory)
        return (NULL);  // Return NULL to indicate allocation failure
    i = 0;  // Initialize counter to first index
    while (i < size)  // Loop through each element (0 to size-1)
    {
        arr[i] = i;  // Set element at index i to value i (0, 1, 2, ..., size-1)
        i++;  // Move to next index
    }
    return (arr);  // Return pointer to first element of newly allocated array
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 20 | `#include <stdlib.h>` | Include the standard library header for memory functions like malloc |
| 22 | `int *ft_malloc_allocator(int size)` | Start of function that creates an int array of given size |
| 24 | `int *arr;` | Declare a pointer that will hold the array's starting memory address |
| 25 | `int i;` | Declare a loop counter variable for iteration |
| 27 | `if (size <= 0)` | Check if the requested size is zero or negative (invalid) |
| 28 | `return (NULL);` | Exit early with NULL to signal invalid input |
| 29 | `arr = malloc(size * sizeof(int));` | Allocate heap memory: number_of_elements × bytes_per_integer |
| 30 | `if (arr == NULL)` | Check if malloc failed (system has no memory available) |
| 31 | `return (NULL);` | Exit with NULL to signal allocation failure to caller |
| 32 | `i = 0;` | Start counter at the first array index (0) |
| 33 | `while (i < size)` | Loop while counter is less than size (runs size times) |
| 35 | `arr[i] = i;` | Store value i at position i (element gets its own index as value) |
| 36 | `i++;` | Advance counter to next index |
| 38 | `return (arr);` | Give caller the pointer to the newly created array |

## Common Traps
- ❌ Forgetting to check for NULL return from malloc.
- ❌ Using wrong size calculation (forgetting `sizeof`).
- ❌ Not handling size <= 0 case.
- ❌ Not initializing all elements.

## Related Concepts
- 01_Concepts/malloc|malloc/free
- 07_Manual/c_stdlib.h|stdlib.h

## Related Exercises
- [[ft_arrs_swap]]
- [[ft_rev_arrays]]
- [[ft_sort_arr_int]]

How do you allocate an array of integers?
::
```c
int *arr = malloc(size * sizeof(int));
if (!arr) return NULL;
```
