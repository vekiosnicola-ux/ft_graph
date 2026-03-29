---
tags: []
date: 2026-03-29
status: complete
---
# ft_foreach

---
tags: [C11, red]
---

## What it does
Applies a given function to every element of an integer array.

## Step-by-step Algorithm
1. Receive an `int *tab`, its `int size`, and a function pointer `void (*f)(int)`.
2. Iterate `i` from 0 to `size - 1`.
3. Call `f(tab[i])` for each element.

## The Code
```c
void ft_foreach(int *tab, int length, void (*f)(int))  // Applies function f to each array element
{
    int i;  // Loop counter for array index

    i = 0;  // Start at first element (index 0)
    while (i < length)  // Loop through all elements (0 to length-1)
    {
        f(tab[i]);  // Call the provided function, passing current element as argument
        i++;        // Move to next array index
    }
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 15 | `void ft_foreach(...)` | Function returns nothing; takes array, length, and function pointer |
| 16 | `int *tab` | Pointer to first element of integer array |
| 16 | `void (*f)(int)` | Function pointer: points to function taking int, returning void |
| 18 | `int i;` | Index variable for iterating through array |
| 20 | `i = 0;` | Initialize index to the first position |
| 21 | `while (i < length)` | Loop condition: continue while index is valid |
| 23 | `f(tab[i]);` | Dereference function pointer and call it with current element |
| 24 | `i++;` | Advance index to next position |

## Common Traps
- ❌ Forgetting to pass the function pointer correctly.
- ❌ Using `i <= length` (off-by-one).
- ❌ Not handling empty array (size = 0).

## Related Concepts
- 01_Concepts/functionPointers|Function Pointers
