---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# ft_list_push_front

---
tags: [C12, red]
---

## Navigation
← C12_INDEX|C12 INDEX | [[ft_list_push_back|Next: ft_list_push_back →]]

## What it does
Adds a new element to the **front** of a linked list. The new element becomes the head of the list.

## The Insight
The key insight is understanding why we need `t_list **begin_list` (double pointer). Since the head pointer is stored in the calling function, we need a pointer-to-pointer to modify it. Think of it like changing the first page of a book - you need to know WHERE the book is stored to update its first page.

## Step-by-step Algorithm
1. Create a new element using `ft_create_elem(data)`
2. Check if allocation succeeded (new_elem != NULL)
3. Point new element's `next` to current head (`*begin_list`)
4. Update head pointer to point to new element (`*begin_list = new_elem`)

## The Code
```c
 <unistd.h>
 "ft_list.h"

void ft_list_push_front(t_list **begin_list, void *data)
{
    t_list *new_elem;  // Declare pointer for new element
    
    new_elem = ft_create_elem(data);  // Create new element with data
    if (new_elem)  // If creation succeeded
    {
        new_elem->next = *begin_list;  // New element points to old head
        *begin_list = new_elem;  // Head now points to new element
    }
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 7 | `void ft_list_push_front(t_list **begin_list, void *data)` | Function takes double pointer to list head and data for new node |
| 9 | `t_list *new_elem;` | Declare pointer to hold new element |
| 11 | `new_elem = ft_create_elem(data);` | Call helper to create new node with data |
| 12 | `if (new_elem)` | Check if malloc succeeded in ft_create_elem |
| 14 | `new_elem->next = *begin_list;` | Link new node's next to current first element (could be NULL if empty list) |
| 15 | `*begin_list = new_elem;` | Update head pointer to new first element |

## Common Traps
- ❌ Using `*begin_list` instead of `**begin_list` (can't modify caller's pointer)
- ❌ Forgetting to link new node to current head before updating head
- ❌ Not checking if `ft_create_elem` returned NULL (malloc failure)
- ❌ Setting `new_elem->next = NULL` instead of pointing to current head
- ❌ Forgetting that an empty list (head=NULL) is handled correctly since NULL->next would be NULL

## Related Concepts
- 01_Concepts/linked_lists|Linked Lists
- 01_Concepts/pointers_to_pointers|Pointer to Pointer
- [[ft_create_elem]]
- [[ft_list_push_back]]
- [[ft_list_size]]

## Related Exercises
- [[ft_create_elem]]
- [[ft_list_push_back]]
- [[ft_list_size]]

How do you add a node to the front of a linked list?
::
1. Create new node with data using `ft_create_elem`
2. Point new node's `next` to current head: `new_elem->next = *begin_list`
3. Update head pointer: `*begin_list = new_elem`
```c
new_elem->next = *begin_list;
*begin_list = new_elem;
```
