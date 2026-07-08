---
tags: [C12, red]
date: 2026-03-29
status: complete
---
# ft_list_find

## Navigation
← [[C12_Index|C12 INDEX]] | [[ft_list_remove_if|Next: ft_list_remove_if →]]

## What it does
Returns a pointer to the first element whose `data` matches the `data_ref` using `cmp` for comparison.

## The Insight
Traverse list comparing each node's data with data_ref using cmp function. Return as soon as you find a match (first occurrence).

## Step-by-step Algorithm
1. Start from the first element.
2. Iterate through the list:
   a. If `cmp(data, data_ref)` returns 0, return the current element.
   b. Move to the next element.
3. Return NULL if no match is found.

## The Code
```c
#include "ft_list.h"  // t_list structure

t_list *ft_list_find(t_list *begin_list, void *data_ref,
                     int (*cmp)())  // Find first matching node
{
    while (begin_list != NULL)                  // Walk the list
    {
        if (cmp(begin_list->data, data_ref) == 0)  // Match found!
            return (begin_list);                // Return pointer to this node
        begin_list = begin_list->next;          // No match: keep looking
    }
    return (NULL);                              // Reached end: nothing matched
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 3-4 | `int (*cmp)()` | Comparison function pointer — returns 0 when data matches |
| 6 | `while (begin_list != NULL)` | Traverse the entire list |
| 8 | `if (cmp(...) == 0)` | Compare current data with reference — 0 means match |
| 9 | `return (begin_list)` | Found it: return pointer to the matching node |
| 10 | `begin_list = begin_list->next` | No match: move to next node |
| 12 | `return (NULL)` | Searched everything: no match found |

## Common Traps
- ❌ Continuing after finding match — should return immediately (first match)
- ❌ Comparing pointers instead of using cmp function
- ❌ Not handling empty list (works: while loop never entered, returns NULL)

## Related Exercises
- [[ft_list_remove_if]]
- [[functionPointers]]
- [[linked_lists]]

How does ft_list_find use a comparison function?
::
It calls `cmp(node->data, data_ref)` for each node. When cmp returns 0 (match), it returns the node pointer. This lets you search with any comparison logic (strcmp, custom, etc.).
