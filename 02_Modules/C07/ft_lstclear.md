---
tags: [C07]
---


# ft_lstclear

## Concept
Deletes and frees all elements of the list using the `del` function, and sets the list pointer to NULL.

## Function Signature
```c
void ft_lstclear(t_list **lst, void (*del)(void *));
```

## Parameters
- `lst`: Pointer to the pointer of the list head
- `del`: Function pointer to free the content

## Return Value
- `void`

## Implementation

```c
 <stdlib.h> // Provides malloc() and free() for dynamic memory management

typedef struct s_list  // Define the list node structure
{
    void *content;          // Pointer to the data stored in this node
    struct s_list *next;    // Pointer to the next node in the list
} t_list;                  // Type alias for struct s_list

// Function: frees all elements of the list and sets *lst to NULL
void ft_lstclear(t_list **lst, void (*del)(void *))
{
    t_list *next;          // Temporary: stores next element before we free current

    if (!lst || !del)      // Guard: check for NULL pointer-to-list or NULL del function
        return ;            // Cannot proceed without both
    while (*lst)           // Loop while there are still elements to free
    {
        next = (*lst)->next; // SAVE next element BEFORE we free current one
        del((*lst)->content); // Free the content using the provided deletion function
        free(*lst);          // Free the current node's memory
        *lst = next;         // Move to the next element (saved earlier)
    }                       // Loop continues until *lst becomes NULL (end of list)
    *lst = NULL;            // Set the caller's pointer to NULL (important!)
}                           // After this, the list is fully freed and pointer is NULL
```

## Line-by-Line Translation
- `#include <stdlib.h>` — Header for malloc() and free()
- `typedef struct s_list` — Define a structure type for list nodes
- `void *content;` — Payload: can point to any type of data
- `struct s_list *next;` — Link to the next node in the list
- `void ft_lstclear(t_list **lst, void (*del)(void *))` — Delete entire list and set to NULL
- `t_list *next;` — Temporary pointer to save next element before freeing
- `if (!lst || !del) return ;` — Guard: need valid pointer-to-list and del function
- `while (*lst)` — Loop while there are elements to free
- `next = (*lst)->next;` — Save the next element before we lose the pointer
- `del((*lst)->content);` — Free the content using user-provided function
- `free(*lst);` — Free the current node's memory
- `*lst = next;` — Advance to the next element
- `*lst = NULL;` — Set caller's pointer to NULL (prevents dangling pointer)

## Algorithm
1. Check if `lst` and `del` are valid
2. While `*lst` is not NULL:
   a. Save `next = (*lst)->next`
   b. Apply `del` to `(*lst)->content`
   c. Free `*lst`
   d. Set `*lst` to `next`
3. Set `*lst` to NULL

## Key Points
- Save `next` BEFORE freeing (can't access after free)
- Double pointer needed to set caller's pointer to NULL
- Uses `while (*lst)` pattern

## Common Traps
- ❌ Forgetting to save `next` before freeing
- ❌ Not setting `*lst` to NULL at the end
- ❌ Forgetting to call `del` on each content

## Related
- [[ft_lstdelone]] - Free single element
- [[ft_lstnew]] - Create new element
