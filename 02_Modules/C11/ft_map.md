---
tags: []
date: 2026-03-29
status: complete
---
# ft_map

---
tags: [C11, red]
---

## What it does
Creates a new array by applying a function to each element of an existing array.

## Step-by-step Algorithm
1. Receive an `int *tab`, `int size`, and function `int (*f)(int)`.
2. Allocate memory for the new array: `malloc(size * sizeof(int))`.
3. Iterate `i` from 0 to `size - 1`.
4. Set `new_tab[i] = f(tab[i])`.
5. Return `new_tab`.

## The Code
```c
 <stdlib.h>  // Provides malloc() for dynamic memory allocation

int *ft_map(int *tab, int length, int (*f)(int))  // Creates new array with transformed values
{
    int *new_tab;  // Pointer to newly allocated output array
    int i;         // Loop counter for array indices

    new_tab = malloc(length * sizeof(int));  // Allocate memory for new array
    if (!new_tab)  // Check if malloc failed (returns NULL when out of memory)
        return (NULL);  // Exit early with NULL to signal allocation failure
    i = 0;  // Start at first element (index 0)
    while (i < length)  // Loop through all original elements
    {
        new_tab[i] = f(tab[i]);  // Apply function f to element, store result in new array
        i++;  // Move to next index
    }
    return (new_tab);  // Return pointer to newly created/transformed array
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 18 | `#include <stdlib.h>` | Header for malloc() function |
| 20 | `int *ft_map(...)` | Returns pointer to new array of transformed integers |
| 20 | `int *tab` | Input array: pointer to first element |
| 20 | `int (*f)(int)` | Function pointer: function takes int, returns int |
| 22 | `int *new_tab;` | Will point to the newly allocated output array |
| 25 | `new_tab = malloc(...)` | Request heap memory for output array |
| 26 | `if (!new_tab)` | Check if malloc returned NULL (allocation failed) |
| 27 | `return (NULL);` | Signal failure to caller |
| 29 | `i = 0;` | Initialize index to start |
| 30 | `while (i < length)` | Loop through all elements |
| 31 | `new_tab[i] = f(tab[i]);` | Transform: apply f to input, store in output at same index |
| 32 | `i++;` | Advance to next element |
| 34 | `return (new_tab);` | Give caller the new transformed array |

## Common Traps
- ❌ Forgetting to check if `malloc` failed.
- ❌ Forgetting to allocate `sizeof(int)` per element.
- ❌ Not returning the new array.

## Related Concepts
- 01_Concepts/functionPointers|Function Pointers
- 01_Concepts/malloc|malloc/free
