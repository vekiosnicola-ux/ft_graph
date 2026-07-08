---
tags: [C12, red]
date: 2026-03-29
status: complete
---
# ft_list_push_back

## Navigation
← [[C12_Index|C12 INDEX]] | [[ft_list_clear|Next: ft_list_clear →]]

## What it does
Adds a new element at the end of the list.

## The Insight
Traverse to the last node, then set its `next` to the new element. Special case: if list is empty, the new element becomes the head.

## Step-by-step Algorithm
1. Create a new element using `ft_create_elem`.
2. If `*begin_list` is NULL, set the new element as the first element.
3. Otherwise, traverse to the last element and set its `next` to the new element.

## The Code
```c
#include "ft_list.h"  // t_list and ft_create_elem

void ft_list_push_back(t_list **begin_list, void *data)  // Add to end
{
    t_list *new;  // The new node
    t_list *cur;  // Traversal pointer

    new = ft_create_elem(data);  // Create new node with given data
    if (!new)                    // Malloc failed inside ft_create_elem
        return;
    if (*begin_list == NULL)     // List is empty
    {
        *begin_list = new;       // New node becomes the head
        return;
    }
    cur = *begin_list;           // Start from head
    while (cur->next != NULL)    // Walk to the last node
        cur = cur->next;
    cur->next = new;             // Link last node to new node
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 3 | `t_list **begin_list` | Pointer to pointer: needed to modify head when list is empty |
| 7 | `new = ft_create_elem(data)` | Reuse ft_create_elem for allocation |
| 10-13 | `if (*begin_list == NULL)` | Empty list special case: new node IS the list |
| 15 | `cur = *begin_list` | Start traversal at head |
| 16-17 | `while (cur->next != NULL)` | Walk to last node (same as ft_list_last) |
| 18 | `cur->next = new` | Append: tail's next now points to new node |

## Common Traps
- ❌ Forgetting the empty list case (segfault when traversing NULL list)
- ❌ Using `t_list *` instead of `t_list **` — can't set head when empty

## Related Exercises
- [[ft_list_last]]
- [[ft_create_elem]]
- [[ft_list_push_front]]

What's the difference between push_front and push_back?
::
push_front: set `new->next = *begin_list; *begin_list = new;` (O(1))
push_back: traverse to last node, set `last->next = new;` (O(n))
