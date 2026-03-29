---
tags: [Level_4, exam]
  - linked-list
  - white
---


# ft_list_foreach

## What it does
Applies a function f to the data of each node in a linked list.

## The Insight
Simple traversal. For each node, call f(node->data). Move to next.

## Step-by-step Algorithm
1. While list != NULL
2. (*f)(list->data)
3. list = list->next

## The Code
```c
// ft_list_foreach: Applies function f to each node's data
// Takes: head of list, function pointer f that takes void* and returns void
// Example: f could print the data, modify it, etc.

void ft_list_foreach(t_list *begin_list, void (*f)(void *))
{
    while (begin_list)                      // Loop while node exists
    {
        (*f)(begin_list->data);            // Call function f with current node's data pointer
        begin_list = begin_list->next;     // Advance to next node in list
    }
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 20 | `void ft_list_foreach(t_list *begin_list, void (*f)(void *))` | Takes list head and function pointer |
| 22 | `while (begin_list)` | Loop: continue while current node is not NULL |
| 24 | `(*f)(begin_list->data);` | Dereference f and call it with current node's data pointer |
| 25 | `begin_list = begin_list->next;` | Advance to next node (doesn't modify caller's list pointer) |

## Common Traps
- ❌ Passing wrong thing to f (pass node->data, not the whole node)
- ❌ Not advancing to next (would cause infinite loop - while would never exit)
- ❌ Dereferencing NULL (would crash - while loop protects against this)

## Related
- [[ft_list_remove_if]] - list removal
- [[sort_list]] - list sorting
- EXAMS INDEX|Exam INDEX
