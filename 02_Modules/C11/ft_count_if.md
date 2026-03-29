---
tags: []
date: 2026-03-29
status: complete
---
# ft_count_if

---
tags: [C11, red]
---

## What it does
Counts how many elements in the array satisfy the given condition.

## Step-by-step Algorithm
1. Receive `char **tab`, `int length`, and function `int (*f)(char*)`.
2. Initialize `count = 0`.
3. Iterate `i` from 0 to `length - 1`.
4. If `f(tab[i])` returns non-zero, increment `count`.
5. Return `count`.

## The Code
```c
int ft_count_if(char **tab, int length, int (*f)(char*))  // Counts elements passing the test
{
    int i;     // Loop counter for array indices
    int count; // Accumulator: number of elements that passed the test

    i = 0;      // Start at first element
    count = 0;  // Initialize counter to zero (no matches yet)
    while (i < length)  // Loop through all strings in array
    {
        if (f(tab[i]))  // Test current element with condition function
            count++;    // Element passed! Increment the counter
        i++;            // Move to next element
    }
    return (count);  // Return total number of passing elements
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 18 | `int ft_count_if(...)` | Returns integer count of elements that pass the test |
| 18 | `char **tab` | Array of strings: pointer to array of char pointers |
| 18 | `int (*f)(char*)` | Function pointer: test function that returns 0=false, non-zero=true |
| 20 | `int i;` | Loop index variable |
| 21 | `int count;` | Accumulator for counting matching elements |
| 23 | `i = 0;` | Start at first index |
| 24 | `count = 0;` | Initialize counter to zero |
| 25 | `while (i < length)` | Loop through all elements |
| 27 | `if (f(tab[i]))` | Call test function on current element |
| 28 | `count++;` | Test returned non-zero (true); add one to counter |
| 29 | `i++;` | Move to next element |
| 31 | `return (count);` | Return the final count of passing elements |

## Common Traps
- ❌ Forgetting to initialize `count` to 0.
- ❌ Not incrementing correctly.
- ❌ Using wrong return type.

## Related Concepts
- 01_Concepts/functionPointers|Function Pointers
