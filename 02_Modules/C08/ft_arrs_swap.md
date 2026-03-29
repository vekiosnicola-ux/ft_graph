---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# ft_arrs_swap

---
tags: [C08, magenta]
---

## Navigation
← [[ft_malloc_allocator|ft_malloc_allocator]] | [[ft_rev_arrays|Next: ft_rev_arrays →]]

## What it does
Swaps the contents of two integer arrays of equal size in place.

## The Insight
Use a temporary variable to hold one element during the swap. Iterate through both arrays simultaneously.

## Step-by-step Algorithm
1. Check if arrays are valid and size > 0.
2. Loop through each index from 0 to `size - 1`.
3. Swap `arr1[i]` with `arr2[i]` using a temporary variable.
4. Return (void).

## The Code
```c
 <stdlib.h>  // Included for consistency (no malloc used here)

void ft_arrs_swap(int *arr1, int *arr2, int size)  // Swaps two arrays element-by-element
{
    int i;     // Loop counter for array indices
    int temp;  // Temporary storage for swap operation

    if (size <= 0 || arr1 == NULL || arr2 == NULL)  // Validate inputs
        return;  // Exit early if invalid: no elements, or null pointers
    i = 0;  // Start at first index (0)
    while (i < size)  // Loop through all elements (0 to size-1)
    {
        temp = arr1[i];  // Save current value from first array into temp
        arr1[i] = arr2[i];  // Copy value from second array into first array
        arr2[i] = temp;  // Copy saved original value into second array
        i++;  // Move to next index position
    }
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 20 | `#include <stdlib.h>` | Include standard library (kept for consistency with other exercises) |
| 22 | `void ft_arrs_swap(...)` | Function returns nothing; modifies both arrays in place |
| 24 | `int i;` | Loop counter to track current array index |
| 25 | `int temp;` | Temporary variable needed because you can't swap without backup |
| 27 | `if (size <= 0 \|\| ...)` | Check for invalid size or NULL pointers |
| 28 | `return;` | Bail out early - nothing to swap |
| 29 | `i = 0;` | Initialize index to start at the beginning |
| 30 | `while (i < size)` | Loop until we've processed all elements |
| 32 | `temp = arr1[i];` | Step 1 of swap: save first array's element in safe place |
| 33 | `arr1[i] = arr2[i];` | Step 2 of swap: copy second array's element into first |
| 34 | `arr2[i] = temp;` | Step 3 of swap: put saved value into second array |
| 35 | `i++;` | Move index forward to process next pair |

## Common Traps
- ❌ Forgetting to use a temporary variable (would lose one value).
- ❌ Not checking for NULL pointers.
- ❌ Swapping only up to wrong index (off-by-one).

## Related Concepts
- 01_Concepts/pointers|Pointers
- 01_Concepts/arrays|Arrays

## Related Exercises
- [[ft_rev_arrays]]
- [[ft_sort_arr_int]]
- [[ft_malloc_allocator]]

How do you swap two arrays?
::
Loop through both arrays, swap each element using temp variable.
