---
tags: [C07]
---


# ft_lstadd_front

## Concept
Adds a new element to the beginning of a linked list.

## Function Signature
```c
void ft_lstadd_front(t_list **lst, t_list *new);
```

## Parameters
- `lst`: Pointer to the pointer of the list head
- `new`: Pointer to the new element to add

## Return Value
- `void`

## Implementation

```c
 <stdlib.h> // Provides malloc() for dynamic memory allocation (if needed)

typedef struct s_list  // Define the list node structure
{
    void *content;          // Pointer to the data stored in this node
    struct s_list *next;    // Pointer to the next node in the list
} t_list;                  // Type alias for struct s_list

// Function: adds new element 'new' to the FRONT (beginning) of the list
void ft_lstadd_front(t_list **lst, t_list *new)
{
    if (!lst || !new)      // Guard: check for NULL list pointer or NULL new element
        return ;            // Cannot add if either is NULL
    new->next = *lst;       // Step 1: Link new element to current first element
    *lst = new;            // Step 2: Update list head to point to new element
}                           // The new element is now the first element (head)
```

## Line-by-Line Translation
- `#include <stdlib.h>` — Header for malloc() (may not be needed here, but often included)
- `typedef struct s_list` — Define a structure type for list nodes
- `void *content;` — Payload: can point to any type of data
- `struct s_list *next;` — Link to the next node in the list
- `void ft_lstadd_front(t_list **lst, t_list *new)` — Add element to front of list
- `if (!lst || !new) return ;` — Guard: need valid pointer-to-list and new element
- `new->next = *lst;` — Make new element point to current first element
- `*lst = new;` — Update the list head pointer to point to the new element

## Algorithm
1. Check if both `lst` and `new` are not NULL
2. Set `new->next` to `*lst` (the current head)
3. Set `*lst` to `new` (new becomes the head)

## Key Points
- Double pointer `t_list **` is needed to modify the caller's pointer
- Link `new->next` BEFORE updating `*lst`
- Order matters: `new->next = *lst` first, then `*lst = new`

## Common Traps
- ❌ Forgetting to link `new->next` before updating `*lst`
- ❌ Passing `t_list *lst` instead of `t_list **lst`

## Related
- [[ft_lstnew]] - Create new element
- [[ft_lstadd_back]] - Add element to back
