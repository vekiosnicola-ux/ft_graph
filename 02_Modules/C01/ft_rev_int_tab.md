---
tags: [C01, flashcard]
---


# ft_rev_int_tab

## What it does
Reverses an integer array in-place using two-pointer technique.

## The Insight
Swap elements from start/end moving toward middle. Two indices: `start` and `end`.

## Step-by-step Algorithm
1. Receive `int *tab`, `int size`
2. `start = 0`, `end = size - 1`
3. While `start < end`:
   a. Swap `tab[start]` and `tab[end]`
   b. `start++`, `end--`

## The Code (with pedagogical comments)
```c
void ft_rev_int_tab(int *tab, int size)  // Function: takes array pointer and size
{
    int start;  // Index for the start of the array
    int end;    // Index for the end of the array
    int temp;   // Temporary variable for swapping

    start = 0;  // Start from the beginning
    end = size - 1;  // End at the last element
    while (start < end)  // Continue until pointers meet in the middle
    {
        temp = tab[start];  // Save the value at start
        tab[start] = tab[end];  // Copy value from end to start
        tab[end] = temp;  // Write saved value to end
        start++;  // Move start pointer forward
        end--;    // Move end pointer backward
    }
}
```

## Line-by-Line Translation
1. `void ft_rev_int_tab(int *tab, int size)` - Define a function that takes an array pointer and its size
2. `int start, end, temp` - Declare indices for start, end, and a temporary for swapping
3. `start = 0` - Initialize start to the first element
4. `end = size - 1` - Initialize end to the last element
5. `while (start < end)` - Continue while start hasn't reached end
6. `temp = tab[start]` - Save the value at the start position
7. `tab[start] = tab[end]` - Copy the value from end to start
8. `tab[end] = temp` - Put the saved value at the end position
9. `start++` - Move the start pointer one step forward
10. `end--` - Move the end pointer one step backward

## Common Traps
- ❌ `end = size` (out of bounds access)
- ❌ Forgetting to update indices (infinite loop)
- ❌ Not using a temporary variable (would lose one value)

## Related Concepts
- 01_Concepts/two_pointer_technique|Two Pointer Technique
- 01_Concepts/in_place_swap|In-Place Swap

## Related Exercises
- [[ft_swap]]
- [[ft_sort_int_tab]]

## Propedeuticity
**Prerequisites:** [[ft_swap]]
**Unlocks:** [[ft_sort_int_tab]]

How do you reverse an array in-place?
::
Use two pointers (start and end), swap elements and move toward the middle:
```c
while (start < end) {
    swap(tab[start], tab[end]);
    start++;
    end--;
}
```
