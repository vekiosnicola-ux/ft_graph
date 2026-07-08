---
tags: [C12, red]
date: 2026-03-29
status: complete
---
# ft_list_remove_if

## Navigation
← [[C12_Index|C12 INDEX]]

## What it does
Removes all elements where `cmp(data, data_ref)` returns 0. Frees the memory of removed elements.

## The Insight
Track previous pointer to relink list when removing nodes. Save next before freeing. Use pointer-to-pointer for clean head removal.

## Step-by-step Algorithm
1. Keep a previous pointer to track the element before the current one.
2. Iterate through the list:
   a. If `cmp(current->data, data_ref)` returns 0:
      - Link previous->next to current->next.
      - Free current's data and element.
      - Move current to next.
   b. Otherwise, update previous to current and move forward.

## The Code
```c
#include <stdlib.h>   // free()
#include "ft_list.h"  // t_list structure

void ft_list_remove_if(t_list **begin_list, void *data_ref,
                       int (*cmp)(), void (*free_fct)(void *))
{
    t_list *cur;  // Current node to examine

    if (!begin_list || !*begin_list)  // Guard: NULL pointer or empty list
        return;
    cur = *begin_list;
    if (cmp(cur->data, data_ref) == 0)  // Head matches → remove head
    {
        *begin_list = cur->next;  // Update head to next node
        free_fct(cur->data);      // Free the data
        free(cur);                // Free the node
        ft_list_remove_if(begin_list, data_ref, cmp, free_fct);  // Check new head
        return;
    }
    // Head doesn't match: recurse on remainder of list
    ft_list_remove_if(&(cur->next), data_ref, cmp, free_fct);
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 4 | `t_list **begin_list` | Pointer-to-pointer: needed to modify head when removing first node |
| 5 | `void (*free_fct)(void *)` | Function to free data (flexible for any data type) |
| 9-10 | `if (!begin_list ...)` | Guard clause: prevent segfaults |
| 12 | `if (cmp(cur->data, data_ref) == 0)` | Does head match? |
| 14-16 | `*begin_list = cur->next; free...` | Unlink head, free it |
| 17 | `ft_list_remove_if(...)` | Recurse: new head might also match |
| 21 | `ft_list_remove_if(&(cur->next), ...)` | Head doesn't match: check rest of list |

## Common Traps
- ❌ Using `t_list *` — can't modify the head pointer itself
- ❌ Not handling consecutive matching nodes (recursion solves this)
- ❌ Accessing freed memory — recursion naturally avoids this
- ❌ Memory leaks — must free both data and node

## Related Exercises
- [[ft_list_find]]
- [[ft_list_clear]]
- [[pointers_to_pointers]]
- [[recursion]]

Why is recursion elegant for ft_list_remove_if?
::
Each recursive call treats `&(cur->next)` as a new list head. If head matches, remove it and recurse again (handles consecutive matches). If not, recurse on the rest. Base case: NULL list → return.
