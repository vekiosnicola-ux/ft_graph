---
tags: [C12, red]
date: 2026-03-29
status: complete
---
# ft_list_clear

## Navigation
← [[C12_Index|C12 INDEX]] | [[ft_list_iter|Next: ft_list_iter →]]

## What it does
Frees all elements of the list and sets the list pointer to NULL.

## The Insight
Save next pointer before freeing current, then move forward. After freeing all, set head to NULL.

## Step-by-step Algorithm
1. Save the current element.
2. Move to the next element before freeing the current one.
3. Repeat until all elements are freed.
4. Set `*begin_list` to NULL.

## The Code
```c
#include <stdlib.h>   // free()
#include "ft_list.h"  // t_list structure

void ft_list_clear(t_list *begin_list, void (*free_fct)(void *))  // Free entire list
{
    t_list *tmp;  // Save next before freeing current

    while (begin_list != NULL)       // While nodes remain
    {
        tmp = begin_list->next;      // Save pointer to NEXT node (before freeing)
        free_fct(begin_list->data);  // Free the data using provided function
        free(begin_list);            // Free the node structure itself
        begin_list = tmp;            // Move to the saved next node
    }
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 5 | `void (*free_fct)(void *)` | Function pointer to free data (flexible for any data type) |
| 9 | `tmp = begin_list->next` | CRITICAL: save next before freeing — can't access freed memory |
| 10 | `free_fct(begin_list->data)` | Free the data payload using the provided function |
| 11 | `free(begin_list)` | Free the node structure itself |
| 12 | `begin_list = tmp` | Move to the saved next node |

## Common Traps
- ❌ Freeing before saving next — `begin_list->next` is garbage after free
- ❌ Not freeing the data — causes memory leaks
- ❌ Only freeing data OR only freeing node — must free both

## Related Exercises
- [[ft_create_elem]]
- [[malloc]]
- [[linked_lists]]

Why must you save `next` before calling free()?
::
Because `free()` releases the memory. After freeing, `begin_list->next` accesses freed memory (undefined behavior). Save `next` first, then free safely.
