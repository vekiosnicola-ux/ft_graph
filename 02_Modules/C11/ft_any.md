---
tags: []
date: 2026-03-29
status: complete
---
# ft_any

---
tags: [C11, red]
---

## What it does
Returns 1 if any element in the array satisfies the given condition, 0 otherwise.

## Step-by-step Algorithm
1. Receive `char **tab`, `int length`, and function `int (*f)(char*)`.
2. Iterate `i` from 0 to `length - 1`.
3. If `f(tab[i])` returns non-zero, return 1.
4. If no element satisfies condition, return 0.

## The Code
```c
int ft_any(char **tab, int length, int (*f)(char*))  // Checks if ANY element satisfies condition
{
    int i;  // Loop counter for array indices

    i = 0;  // Start at first element (index 0)
    while (i < length)  // Loop through all strings in the array
    {
        if (f(tab[i]))  // Call condition function on current string
            return (1);  // Condition met! Return true immediately
        i++;  // Move to next string
    }
    return (0);  // No element satisfied the condition; return false
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 16 | `int ft_any(...)` | Returns 1 (true) if any element passes test, 0 (false) otherwise |
| 17 | `char **tab` | Array of strings: pointer to array of char pointers |
| 17 | `int (*f)(char*)` | Function pointer: takes string, returns int (0=false, non-zero=true) |
| 19 | `int i;` | Index variable for iteration |
| 21 | `i = 0;` | Start at first element |
| 22 | `while (i < length)` | Loop through all strings |
| 24 | `if (f(tab[i]))` | Call test function on current string; non-zero = passes test |
| 25 | `return (1);` | Found an element that passes! Return immediately with true |
| 26 | `i++;` | Not this one; check the next string |
| 28 | `return (0);` | Checked all elements; none passed, return false |

## Common Traps
- ❌ Forgetting to check all elements.
- ❌ Not returning 1 immediately when found.
- ❌ Not handling empty array (return 0).

## Related Concepts
- 01_Concepts/functionPointers|Function Pointers
- 01_Concepts/arrays|Arrays
