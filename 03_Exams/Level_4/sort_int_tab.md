---
tags: [Level_4, exam]
  - algorithm
  - sorting
  - white
---


# sort_int_tab

## What it does
Sorts integer array in ascending order using bubble sort.

## The Insight
Compare adjacent pairs. If out of order, swap and reset i=0 to check again. CRITICAL: loop condition must be i < (size-1), NOT i < size.

## Step-by-step Algorithm
1. i=0, temp
2. While i < (size-1): if tab[i] > tab[i+1]: swap, i=0. else i++
3. This ensures sorted

## The Code
```c
// ft_sort_int_tab: Sorts integer array in-place using bubble sort
// Takes: pointer to array, array size
// Returns: void (sorts in-place)

void ft_sort_int_tab(int *tab, int size)
{
    int i = 0;                             // Current position in array
    int temp;                              // Temporary storage for swapping
    
    while (i < (size - 1))                 // Loop while not at second-to-last element
    {
        if (tab[i] > tab[i + 1])           // If current > next (out of order)
        {
            temp = tab[i];                  // Store current value
            tab[i] = tab[i + 1];           // Copy next value to current position
            tab[i + 1] = temp;            // Copy stored value to next position
            i = 0;                         // RESET i to 0 (must restart scan from beginning)
        }
        else                                // If in correct order
            i++;                           // Move to next position
    }
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 20 | `void ft_sort_int_tab(int *tab, int size)` | Sorts in-place: takes array pointer and size |
| 22 | `int i = 0;` | Initialize index to 0 |
| 23 | `int temp;` | Temporary variable for swapping values |
| 24 | `while (i < (size - 1))` | Loop condition: i must be < size-1 because we access tab[i+1] |
| 26 | `if (tab[i] > tab[i + 1])` | Compare adjacent elements: if left > right, they're out of order |
| 27 | `temp = tab[i];` | Step 1 of 3-way swap: save left value |
| 28 | `tab[i] = tab[i + 1];` | Step 2: overwrite left with right value |
| 29 | `tab[i + 1] = temp;` | Step 3: write saved left value to right position |
| 30 | `i = 0;` | CRITICAL: reset i to 0 after any swap to re-scan from beginning |
| 32-33 | `else i++;` | If in correct order, advance to next position |

## Common Traps
- ❌ Using i < size (accesses tab[size], segfault - we compare with i+1 so max i is size-2)
- ❌ Not resetting i=0 after swap (algorithm wouldn't re-check earlier elements, could miss swaps)
- ❌ Wrong swap order (temp must save original value before overwriting)

## Related
- [[sort_list]] - linked list sorting
- [[fprime]] - prime factors
- EXAMS INDEX|Exam INDEX
