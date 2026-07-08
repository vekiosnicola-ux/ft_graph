---
tags: [C12, red]
date: 2026-03-29
status: complete
---
# ft_list_size

## Navigation
← [[C12_Index|C12 INDEX]] | [[ft_list_last|Next: ft_list_last →]]

## What it does
Counts and returns the number of elements in the linked list.

## The Insight
Traverse the list from head to tail, counting nodes until you reach NULL.

## Step-by-step Algorithm
1. Start from the first element (`begin_list`).
2. Initialize a counter to 0.
3. Iterate through the list: while current element is not NULL, increment counter and move to next.
4. Return the counter.

## The Code
```c
#include "ft_list.h"  // t_list structure definition

int ft_list_size(t_list *begin_list)  // Count nodes in the list
{
    int size;  // Running counter

    size = 0;                          // Start at zero
    while (begin_list != NULL)         // While there's still a node
    {
        size++;                        // Count this node
        begin_list = begin_list->next; // Advance to next node
    }
    return (size);                     // Return total count
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 3 | `int ft_list_size(t_list *begin_list)` | Takes head pointer, returns int count |
| 5 | `int size;` | Counter variable |
| 7 | `size = 0;` | Initialize counter to zero |
| 8 | `while (begin_list != NULL)` | Loop until end of list (NULL) |
| 10 | `size++;` | Found a node: increment |
| 11 | `begin_list = begin_list->next;` | Move to next node in chain |
| 13 | `return (size);` | Return total node count |

## Common Traps
- ❌ Forgetting NULL list returns 0 (works correctly: loop never entered)
- ❌ Off-by-one: checking `->next != NULL` would miss last element

## Related Exercises
- [[ft_list_last]]
- [[ft_create_elem]]
- [[linked_lists]]

How do you count elements in a linked list?
::
Traverse with `while (node != NULL)`, incrementing a counter each step. Return the counter.
