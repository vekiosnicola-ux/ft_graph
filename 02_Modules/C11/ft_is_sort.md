---
tags: []
date: 2026-03-29
status: complete
---
# ft_is_sort

---
tags: [C11, red]
---

## What it does
Returns 1 if the array is sorted in ascending or descending order, 0 otherwise.

## Step-by-step Algorithm
1. Receive `int *tab`, `int length`, and comparison function `int (*f)(int, int)`.
2. If `length <= 1`, return 1.
3. Check ascending: iterate `i` from 0 to `length - 2`, if `f(tab[i], tab[i+1]) > 0`, not sorted.
4. Check descending: iterate `i` from 0 to `length - 2`, if `f(tab[i], tab[i+1]) < 0`, not sorted.
5. Return 1 if sorted in either direction, 0 otherwise.

## The Code
```c
int ft_is_sort(int *tab, int length, int (*f)(int, int))  // Checks if array is sorted
{
    int i;   // Loop counter for adjacent pair comparisons
    int asc;  // Flag: 1 if ascending order maintained so far
    int desc; // Flag: 1 if descending order maintained so far

    if (length <= 1)  // Arrays with 0 or 1 element are always considered sorted
        return (1);  // Trivially sorted
    i = 0;  // Start comparing from the first adjacent pair
    asc = 1;  // Assume sorted ascending until proven otherwise
    desc = 1; // Assume sorted descending until proven otherwise
    while (i < length - 1)  // Check all adjacent pairs: (0,1), (1,2), ..., (length-2, length-1)
    {
        if (f(tab[i], tab[i + 1]) > 0)  // If current pair fails ascending test (should be <=)
            asc = 0;  // Ascending order violated; mark as not ascending
        if (f(tab[i], tab[i + 1]) < 0)  // If current pair fails descending test (should be >=)
            desc = 0;  // Descending order violated; mark as not descending
        i++;  // Move to next adjacent pair
    }
    return (asc || desc);  // Return 1 if sorted in either direction, 0 if not sorted at all
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 18 | `int ft_is_sort(...)` | Returns 1 if sorted, 0 if not sorted |
| 18 | `int (*f)(int, int)` | Comparison function: returns negative if a<b, 0 if a==b, positive if a>b |
| 20 | `int i;` | Index for comparing adjacent pairs |
| 21 | `int asc;` | Flag tracking if ascending order is maintained |
| 22 | `int desc;` | Flag tracking if descending order is maintained |
| 24 | `if (length <= 1)` | Empty or single-element arrays are trivially sorted |
| 25 | `return (1);` | No need to check further; it's sorted |
| 26 | `i = 0;` | Start at first element |
| 27 | `asc = 1;` | Assume ascending until we find evidence otherwise |
| 28 | `desc = 1;` | Assume descending until we find evidence otherwise |
| 29 | `while (i < length - 1)` | Loop through all adjacent pairs |
| 31 | `if (f(tab[i], tab[i + 1]) > 0)` | Comparison says element i > element i+1 |
| 32 | `asc = 0;` | Ascending order is broken here |
| 34 | `if (f(tab[i], tab[i + 1]) < 0)` | Comparison says element i < element i+1 |
| 35 | `desc = 0;` | Descending order is broken here |
| 37 | `return (asc \|\| desc);` | Array is sorted if either direction flag is still true |

## Common Traps
- ❌ Not handling empty or single-element arrays.
- ❌ Only checking one direction.
- ❌ Not resetting flags correctly.

## Related Concepts
- 01_Concepts/functionPointers|Function Pointers
- 01_Concepts/sorting|Sorting Algorithms
