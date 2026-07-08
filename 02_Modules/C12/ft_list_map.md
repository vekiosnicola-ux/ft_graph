---
tags: [C12, red]
date: 2026-03-29
status: complete
---
# ft_list_map

## Navigation
← [[C12_Index|C12 INDEX]] | [[ft_list_find|Next: ft_list_find →]]

## What it does
Creates a new list by applying function `f` to each element's `data` in the original list. The new list is returned.

## The Insight
Create new nodes with transformed data, preserving list structure. The original list is NOT modified.

## Step-by-step Algorithm
1. If `begin_list` is NULL, return NULL.
2. Create the first new element with `f(begin_list->data)`.
3. Store the head of the new list.
4. Iterate through original list, creating new elements and linking them.
5. Return the head of the new list.

## The Code
```c
#include "ft_list.h"  // t_list and ft_create_elem

t_list *ft_list_map(t_list *begin_list, void *(*f)(void *))  // Map function over list
{
    t_list *new_list;  // Head of the new list
    t_list *cur;       // Current node in new list (for linking)

    if (!begin_list)                           // Empty list → return NULL
        return (NULL);
    new_list = ft_create_elem(f(begin_list->data));  // First new node
    if (!new_list)                             // Malloc failed
        return (NULL);
    cur = new_list;                            // cur tracks tail of new list
    begin_list = begin_list->next;             // Move to second original node
    while (begin_list != NULL)                 // Process remaining nodes
    {
        cur->next = ft_create_elem(f(begin_list->data));  // Create & link
        if (!cur->next)                        // Malloc failed
            return (new_list);                 // Return partial list (or free all)
        cur = cur->next;                       // Advance new list tail
        begin_list = begin_list->next;         // Advance original list
    }
    return (new_list);                         // Return head of new list
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 3 | `void *(*f)(void *)` | Function pointer: takes void*, returns void* (transformed data) |
| 8-9 | `new_list = ft_create_elem(f(...))` | Create first node with transformed data |
| 11 | `cur = new_list` | cur starts at head, will track the tail |
| 14-20 | `while (begin_list)` | Walk original, creating new nodes |
| 16 | `cur->next = ft_create_elem(...)` | Create node and link to previous new node |
| 18 | `cur = cur->next` | Advance tail tracker |

## Common Traps
- ❌ Not checking malloc failure for each new node
- ❌ Modifying original list data (f returns NEW data, original is untouched)
- ❌ Losing track of new list head (must save it before advancing)

## Related Exercises
- [[ft_list_iter]]
- [[ft_create_elem]]
- [[functionPointers]]

How does ft_list_map differ from ft_list_iter?
::
`ft_list_map` creates a NEW list with `f(data)` for each node, preserving the original. `ft_list_iter` modifies data in-place on the same list.
