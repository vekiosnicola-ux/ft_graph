---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# ft_create_elem

---
tags: [C12, red]
---

## Navigation
← C12_INDEX|C12 INDEX | [[ft_list_push_front|Next: ft_list_push_front →]]

## What it does
Creates a new element of type `t_list`, initializes its `data` with the given parameter, and sets `next` to NULL.

## The Insight
A linked list node contains data and a pointer to the next element. Using `malloc` allocates memory for the node structure.

## Step-by-step Algorithm
1. Allocate memory for a new element using `malloc`.
2. If allocation fails, return NULL.
3. Set the `data` field to the provided parameter.
4. Set the `next` field to NULL.
5. Return the new element.

## The Code
```c
 <stdlib.h>   // Provides malloc() for dynamic memory allocation
 "ft_list.h"  // Header defining t_list structure

t_list *ft_create_elem(void *data)  // Creates and returns a new linked list node
{
    t_list *elem;  // Pointer to the newly allocated node structure

    elem = malloc(sizeof(t_list));  // Request memory for one t_list structure
    if (!elem)  // Check if malloc failed (returns NULL when out of memory)
        return (NULL);  // Exit early with NULL to signal allocation failure
    elem->data = data;  // Store the provided data pointer in this node
    elem->next = NULL;  // This is the last node; no next element yet
    return (elem);  // Return pointer to the newly created node
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 23 | `#include <stdlib.h>` | Header for malloc() and free() functions |
| 24 | `#include "ft_list.h"` | Local header defining the t_list structure |
| 26 | `t_list *ft_create_elem(void *data)` | Creates one list node; data can be any pointer type |
| 28 | `t_list *elem;` | Will point to newly allocated node after malloc succeeds |
| 30 | `elem = malloc(sizeof(t_list));` | Allocate exact bytes needed for one t_list structure |
| 31 | `if (!elem)` | Shorthand: true when malloc returned NULL (allocation failed) |
| 32 | `return (NULL);` | Tell caller memory allocation failed |
| 33 | `elem->data = data;` | Arrow operator: store data in the node's data field |
| 34 | `elem->next = NULL;` | New node has no successor; this will be the tail until linked |
| 35 | `return (elem);` | Give caller the new node; they can link it or use directly |

## Common Traps
- ❌ Forgetting to check malloc return.
- ❌ Not setting next to NULL.
- ❌ Using wrong sizeof.

## Related Concepts
- 01_Concepts/linked_lists|Linked Lists
- 01_Concepts/malloc|malloc/free
- 01_Concepts/structures|Structures

## Related Exercises
- [[ft_list_push_front]]
- [[ft_list_push_back]]
- [[ft_list_size]]

How do you create a linked list node?
::
```c
t_list *elem = malloc(sizeof(t_list));
elem->data = data;
elem->next = NULL;
return (elem);
```
