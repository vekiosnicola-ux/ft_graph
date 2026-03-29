---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# ft_sort_arr_int

---
tags: [C08, magenta]
---

## Navigation
← [[ft_rev_arrays|ft_rev_arrays]] | [[ft_sqrt|Next: ft_sqrt →]]

## What it does
Sorts an array of integers in ascending order using bubble sort.

## The Insight
Repeatedly compare adjacent elements and swap if out of order. Reset index to 0 after each swap to ensure full sorting.

## Step-by-step Algorithm
1. Check if array is valid and size > 1.
2. Initialize index `i = 0`.
3. While `i < size - 1`:
   a. If `arr[i] > arr[i + 1]`, swap them.
   b. After swap, reset `i = 0`.
   c. Else, increment `i`.
4. Return (void).

## The Code
```c
 <stdlib.h>  // Included for consistency (no malloc used here)

void ft_sort_arr_int(int *arr, int size)  // Sorts array using bubble sort algorithm
{
    int i;     // Current position being examined in this pass
    int temp;  // Temporary storage for swapping two values

    if (size <= 1 || arr == NULL)  // Arrays with 0 or 1 element are already sorted
        return;  // Exit early - nothing to sort
    i = 0;  // Start examining from the first position
    while (i < size - 1)  // Maximum number of adjacent pairs to check
    {
        if (arr[i] > arr[i + 1])  // If current element is bigger than next element
        {
            temp = arr[i];  // Save the larger (left) value temporarily
            arr[i] = arr[i + 1];  // Put smaller (right) value on the left
            arr[i + 1] = temp;  // Put larger saved value on the right
            i = 0;  // RESTART from beginning after any swap (bubble sort rule)
        }
        else
            i++;  // No swap needed, move forward to check next pair
    }
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 23 | `#include <stdlib.h>` | Include standard library header |
| 25 | `void ft_sort_arr_int(...)` | Modifies array in place, returns nothing |
| 27 | `int i;` | Position tracker for current comparison |
| 28 | `int temp;` | Holding spot when swapping two array values |
| 30 | `if (size <= 1 \|\| arr == NULL)` | Check: 0 or 1 elements need no sorting |
| 31 | `return;` | Already sorted or invalid - exit immediately |
| 32 | `i = 0;` | Start fresh from the first position |
| 33 | `while (i < size - 1)` | Loop through adjacent pairs (0-1, 1-2, ..., size-2 to size-1) |
| 35 | `if (arr[i] > arr[i + 1])` | Test if left element is greater than right element |
| 36-40 | (swap block) | Three-step swap using temp variable |
| 40 | `i = 0;` | KEY: After ANY swap, restart from beginning to ensure full sorting |
| 43 | `i++;` | If no swap at this position, move to next pair |

## Common Traps
- ❌ Using `i < size` (would access out of bounds).
- ❌ Not resetting `i` after a swap.
- ❌ Forgetting to increment `i` when no swap.

## Related Concepts
- 01_Concepts/bubble_sort|Bubble Sort
- 01_Concepts/arrays|Arrays

## Related Exercises
- [[ft_rev_arrays]]
- [[ft_arrs_swap]]

How does bubble sort work?
::
Compare adjacent elements, swap if out of order, reset to start after each swap.
