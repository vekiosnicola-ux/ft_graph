---
tags: [C12, red]
date: 2026-03-29
status: complete
---
# ft_list_last

## Navigation
← [[C12_Index|C12 INDEX]] | [[ft_list_push_front|Next: ft_list_push_front →]]

## What it does
Returns a pointer to the last element of the list.

## The Insight
Traverse the list until `next` is NULL - that's the last element.

## Step-by-step Algorithm
1. If the list is empty, return NULL.
2. Start from the first element.
3. Iterate through the list until `next` is NULL.
4. Return the current element (which is the last one).

## The Code
```c
#include "ft_list.h"  // t_list structure definition

t_list *ft_list_last(t_list *begin_list)  // Return pointer to last node
{
    if (!begin_list)               // Empty list: no last element
        return (NULL);
    while (begin_list->next != NULL)  // While NOT at the last node
        begin_list = begin_list->next; // Move forward
    return (begin_list);           // This node's next is NULL: it's the last
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 3 | `t_list *ft_list_last(t_list *begin_list)` | Returns pointer to last node |
| 5-6 | `if (!begin_list) return (NULL)` | Guard: empty list → return NULL |
| 7 | `while (begin_list->next != NULL)` | Keep going while there's a next node |
| 8 | `begin_list = begin_list->next` | Advance to that next node |
| 9 | `return (begin_list)` | Loop ended: we're at the last node |

## Common Traps
- ❌ Checking `begin_list != NULL` instead of `begin_list->next != NULL` — would go past the last node
- ❌ Not handling empty list (segfault on `NULL->next`)

## Related Exercises
- [[ft_list_size]]
- [[ft_list_push_back]]
- [[linked_lists]]

How do you find the last element of a linked list?
::
`while (node->next != NULL) node = node->next;` — stop when next is NULL, return the current node.
