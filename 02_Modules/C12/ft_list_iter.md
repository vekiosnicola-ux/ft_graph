---
tags: [C12, red]
date: 2026-03-29
status: complete
---
# ft_list_iter

## Navigation
← [[C12_Index|C12 INDEX]] | [[ft_list_map|Next: ft_list_map →]]

## What it does
Applies the function `f` to each element's `data` in the list.

## The Insight
Simple traversal: start at head, apply f to data, move to next until NULL. This is the list equivalent of a `for` loop over an array.

## Step-by-step Algorithm
1. Start from the first element.
2. While current element is not NULL:
   a. Apply function `f` to `current->data`.
   b. Move to the next element.

## The Code
```c
#include "ft_list.h"  // t_list structure

void ft_list_iter(t_list *begin_list, void (*f)(void *))  // Apply f to each node's data
{
    while (begin_list != NULL)         // While nodes remain
    {
        f(begin_list->data);           // Apply function to this node's data
        begin_list = begin_list->next; // Move to next node
    }
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 3 | `void (*f)(void *)` | Function pointer: takes void*, returns void |
| 5 | `while (begin_list != NULL)` | Traverse entire list |
| 7 | `f(begin_list->data)` | Call function f with current node's data |
| 8 | `begin_list = begin_list->next` | Advance to next node |

## Common Traps
- ❌ Not handling NULL list (works: while loop never entered)
- ❌ Modifying the list structure during iteration (only modify data, not links)

## Related Exercises
- [[ft_list_map]]
- [[functionPointers]]
- [[linked_lists]]

What's the difference between ft_list_iter and ft_list_map?
::
`ft_list_iter` modifies data in-place (void return). `ft_list_map` creates a NEW list with transformed data (returns t_list*).
