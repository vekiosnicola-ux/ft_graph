---
tags: [C01, flashcard]
---


# ft_sort_int_tab

## What it does
Sorts an integer array in ascending order using bubble sort.

## The Insight
Bubble sort: compare adjacent elements, swap if needed. Reset to start after each swap to ensure full sorting.

## Step-by-step Algorithm
1. Receive `int *tab`, `int size`
2. `i = 0`
3. While `i < size - 1`:
   a. If `tab[i] > tab[i+1]`: swap, reset `i = 0`
   b. Else: `i++`

## The Code (with pedagogical comments)
```c
void ft_sort_int_tab(int *tab, int size)  // Function: takes array pointer and size
{
    int i;    // Current index
    int temp;  // Temporary variable for swapping

    i = 0;  // Start at the beginning
    while (i < (size - 1))  // Continue while there are pairs to compare
    {
        if (tab[i] > tab[i + 1])  // If adjacent elements are out of order
        {
            temp = tab[i];  // Save the value at position i
            tab[i] = tab[i + 1];  // Swap: put smaller value at position i
            tab[i + 1] = temp;  // Put larger value at position i+1
            i = 0;  // Reset to beginning to check all pairs again
        }
        else
            i++;  // If ordered, move to next pair
    }
}
```

## Line-by-Line Translation
1. `void ft_sort_int_tab(int *tab, int size)` - Define a function that takes an array pointer and its size
2. `int i, temp` - Declare index and temporary variable for swapping
3. `i = 0` - Start at the beginning of the array
4. `while (i < (size - 1))` - Loop while there are still pairs to compare
5. `if (tab[i] > tab[i + 1])` - Check if current pair is out of order
6. `temp = tab[i]` - Save the value at position i
7. `tab[i] = tab[i + 1]` - Move the smaller value forward
8. `tab[i + 1] = temp` - Move the larger value backward
9. `i = 0` - Reset index to start checking from the beginning again
10. `else i++` - If pair was in order, move to the next pair

## Common Traps
- ❌ `i < size` (out of bounds access to tab[i+1])
- ❌ Not resetting i after swap (would miss earlier elements)
- ❌ Forgetting to increment when no swap (infinite loop)

## Related Concepts
- 01_Concepts/bubble_sort|Bubble Sort
- 01_Concepts/sorting_algorithms|Sorting Algorithms

## Related Exercises
- [[ft_rev_int_tab]]
- [[ft_swap]]

## Propedeuticity
**Prerequisites:** [[ft_rev_int_tab]], [[ft_swap]]
**Unlocks:** Exam sorting questions, C03+

How does bubble sort work?
::
Repeatedly step through the list, compare adjacent elements, and swap if out of order. After each full pass, the largest unsorted element "bubbles up" to its correct position. Reset to start after each swap to ensure complete sorting.
