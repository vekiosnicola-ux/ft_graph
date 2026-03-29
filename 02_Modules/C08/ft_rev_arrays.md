---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# ft_rev_arrays

---
tags: [C08, magenta]
---

## Navigation
← [[ft_arrs_swap|ft_arrs_swap]] | [[ft_sort_arr_int|Next: ft_sort_arr_int →]]

## What it does
Reverses an array of integers in place.

## The Insight
Use two indices (start and end) moving toward the center. Swap elements at these indices until they meet.

## Step-by-step Algorithm
1. Check if array is valid and size > 0.
2. Initialize `start = 0` and `end = size - 1`.
3. While `start < end`:
   a. Swap `arr[start]` with `arr[end]`.
   b. Increment `start`, decrement `end`.
4. Return (void).

## The Code
```c
 <stdlib.h>  // Included for consistency (no malloc used here)

void ft_rev_arrays(int *arr, int size)  // Reverses array by swapping ends moving inward
{
    int start;  // Index starting from the left (beginning) of array
    int end;    // Index starting from the right (end) of array
    int temp;   // Temporary storage for swapping two values

    if (size <= 0 || arr == NULL)  // Validate inputs
        return;  // Exit if array is empty/invalid
    start = 0;  // Left pointer starts at first element
    end = size - 1;  // Right pointer starts at last element
    while (start < end)  // Continue until pointers meet or cross
    {
        temp = arr[start];  // Save left element before overwriting
        arr[start] = arr[end];  // Copy right element to left position
        arr[end] = temp;  // Put saved left element at right position
        start++;  // Move left pointer rightward (toward center)
        end--;    // Move right pointer leftward (toward center)
    }
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 22 | `#include <stdlib.h>` | Include standard library header (conventional for array exercises) |
| 24 | `void ft_rev_arrays(...)` | Function returns nothing; modifies array directly in memory |
| 26 | `int start;` | Left-side index that will move from 0 toward center |
| 27 | `int end;` | Right-side index that will move from size-1 toward center |
| 28 | `int temp;` | Temporary holding spot needed to swap two values safely |
| 30 | `if (size <= 0 \|\| arr == NULL)` | Reject invalid inputs: no elements or null pointer |
| 31 | `return;` | Exit immediately - nothing to reverse |
| 32 | `start = 0;` | Initialize left pointer to first element index |
| 33 | `end = size - 1;` | Initialize right pointer to last element index |
| 34 | `while (start < end)` | Keep going while the two pointers haven't met/crossed |
| 36 | `temp = arr[start];` | Save the left-side value before it gets overwritten |
| 37 | `arr[start] = arr[end];` | Copy right-side value to the left position |
| 38 | `arr[end] = temp;` | Put the saved left value into the right position |
| 39 | `start++;` | Move left pointer one step toward the center |
| 40 | `end--;` | Move right pointer one step toward the center |

## Common Traps
- ❌ Using `end = size` (would be out of bounds).
- ❌ Not checking `start < end` (could cause issues).
- ❌ Forgetting to increment/decrement indices (infinite loop).

## Related Concepts
- 01_Concepts/pointers|Pointers
- 01_Concepts/arrays|Arrays

## Related Exercises
- [[ft_arrs_swap]]
- [[ft_sort_arr_int]]

How do you reverse an array in place?
::
Use two pointers (start/end), swap until they meet.
