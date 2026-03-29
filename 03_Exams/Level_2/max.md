---
tags: [Level_2, exam]
  - maximum
Level: 2
Topic: Array Manipulation
Exercise: max
---


# max

## What It Does
Returns the maximum value in an array of integers.

## The Insight
Simple linear scan. Track the current max value, compare each element, update when a larger one is found.

## Step-by-Step Algorithm
1. `max = tab[0]`
2. Iterate `i` from 1 to `size-1`
3. If `tab[i] > max`, update max
4. Return max

## Code
```c
int max(int *tab, int size)                     // Function: takes int pointer and array size, returns int
{
    int max = tab[0];                           // Initialize max to first element of the array
    int i = 1;                                  // Start from second element (index 1)

    while (i < size)                            // Loop through remaining elements
    {
        if (tab[i] > max)                        // If current element exceeds current max
            max = tab[i];                        // Update max to the current element
        i++;                                     // Move to next element
    }

    return max;                                  // Return the maximum value found
}
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int max(int *tab, int size)` | Define function: takes int array pointer and size, returns int |
| `{` | Start of function body |
| `int max = tab[0];` | Initialize max to the first element of the array |
| `int i = 1;` | Set starting index to 1 (second element) |
| `while (i < size)` | Loop while index is within array bounds |
| `{` | Start of while body |
| `if (tab[i] > max)` | Check if current element is greater than current max |
| `max = tab[i];` | Update max to the current element |
| `i++;` | Increment index to check next element |
| `}` | End of while loop |
| `return max;` | Return the maximum value found |
| `}` | End of function |

## Common Traps
- ❌ Passing `size=0` (segfault trying to read `tab[0]`)
- ❌ Not initializing max to `tab[0]` (using uninitialized variable)
- ❌ Forgetting to return the max value
- ❌ Off-by-one: starting loop at 0 instead of 1 (would compare tab[0] to itself)

## Related Exercises
- [[ft_sort_int_tab]] - Array sorting
- [[max]] - Array minimum (similar logic, just flip comparison)

## Wiki Links
03_Exams/Level_2_INDEX|Level 2 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 78 lines)
