---
tags: [Level_3, exam]
  - reverse-order
  - white
Level: 3
Topic: Memory Management
Exercise: ft_rrange
---


# ft_rrange

## What It Does
Like ft_range but fills the array in REVERSE order. If `start=1`, `end=3`, array = `[3, 2, 1]`.

## The Insight
Same as ft_range but you fill by decrementing from end to start, rather than incrementing from start to end.

## Step-by-Step Algorithm
1. `len = abs(start - end) + 1`
2. `malloc(len * sizeof(int))`
3. Fill array by decrementing from end to start
4. Return array

## Code
```c
int *ft_rrange(int start, int end)              // Function: takes start and end, returns int array
{
    int *result;                                 // Pointer for result array
    int len = abs(start - end) + 1;             // Calculate length (absolute difference + 1)

    result = malloc(len * sizeof(int));         // Allocate memory for array (size * sizeof(int))
    int i = 0;                                  // Initialize loop counter

    while (i < len)                             // Loop through array positions
    {
        result[i] = end;                         // Store current end value at position i
        i++;                                     // Move to next position
        end--;                                   // Decrement end value for next iteration
    }

    return result;                               // Return pointer to allocated array
}
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int *ft_rrange(int start, int end)` | Define function: takes start and end, returns int array pointer |
| `{` | Start of function body |
| `int *result;` | Declare pointer for result array |
| `int len = abs(start - end) + 1;` | Calculate length: absolute difference plus 1 |
| `result = malloc(len * sizeof(int));` | Allocate memory: length times size of int |
| `int i = 0;` | Initialize loop counter to 0 |
| `while (i < len)` | Loop through array positions |
| `{` | Start of while body |
| `result[i] = end;` | Store current end value at position i |
| `i++;` | Move to next position |
| `end--;` | Decrement end for next iteration |
| `}` | End of while body |
| `return result;` | Return pointer to allocated array |
| `}` | End of function |

## Common Traps
- ❌ Wrong order of filling (filling ascending instead of descending)
- ❌ Forgetting to multiply by sizeof(int) in malloc (allocates wrong size)
- ❌ Not using abs() for length calculation (could get negative)
- ❌ Forgetting to check malloc return value

## Related Exercises
- [[ft_range]] - Original range allocation (ascending order)
- [[ft_strdup]] - Memory allocation basics

## Wiki Links
03_Exams/Level_3_INDEX|Level 3 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 50 lines)
