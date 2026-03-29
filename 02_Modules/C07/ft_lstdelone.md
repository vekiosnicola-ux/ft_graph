---
tags: [C07]
---


# ft_lstdelone

## Concept
Frees the memory of a single list element's content using a deletion function, then frees the element itself.

## Function Signature
```c
void ft_lstdelone(t_list *lst, void (*del)(void *));
```

## Parameters
- `lst`: Pointer to the element to delete
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

// Function: frees the memory of a single list element (content + node)
void ft_lstdelone(t_list *lst, void (*del)(void *))
{
    if (!lst || !del)      // Guard: check for NULL element or NULL del function
        return ;            // Nothing to free if either is NULL
    del(lst->content);     // Step 1: Free the content using user-provided function
    free(lst);             // Step 2: Free the node's memory itself
}                           // Note: does NOT free subsequent elements (only this one)
```

## Line-by-Line Translation
- `#include <stdlib.h>` — Header for malloc() and free()
- `typedef struct s_list` — Define a structure type for list nodes
- `void *content;` — Payload: can point to any type of data
- `struct s_list *next;` — Link to the next node in the list
- `void ft_lstdelone(t_list *lst, void (*del)(void *))` — Delete/free one list element
- `if (!lst || !del) return ;` — Guard: exit early if element or function is NULL
- `del(lst->content);` — Free the content using the user-provided deletion function
- `free(lst);` — Free the memory of the node structure itself

## Algorithm
1. Check if `lst` and `del` are not NULL
2. Call `del(lst->content)` to free the content
3. Call `free(lst)` to free the element

## Key Points
- Uses `del` function pointer to free content (content could be any type)
- Order matters: call `del` BEFORE `free`
- Only frees the element, not the rest of the list

## Common Traps
- ❌ Forgetting to call `del` on `lst->content` before freeing
- ❌ Freeing before using `del`
- ❌ Not checking if `lst` or `del` is NULL

## Related
- [[ft_lstclear]] - Free entire list
- [[ft_lstnew]] - Create new element
