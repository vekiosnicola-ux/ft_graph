---
tags: [C07]
---


# ft_lstadd_back

## Concept
Adds a new element to the end of a linked list.

## Function Signature
```c
void ft_lstadd_back(t_list **lst, t_list *new);
```

## Parameters
- `lst`: Pointer to the pointer of the list head
- `new`: Pointer to the new element to add

## Return Value
- `void`

## Implementation

```c
typedef struct s_list  // Define the list node structure
{
    void *content;          // Pointer to the data stored in this node
    struct s_list *next;    // Pointer to the next node in the list
} t_list;                  // Type alias for struct s_list

// Function: adds new element 'new' to the END of the list
void ft_lstadd_back(t_list **lst, t_list *new)
{
    t_list *last;           // Temporary pointer to find the last element

    if (!lst || !new)      // Guard: check for NULL list pointer or NULL new element
        return ;            // Cannot add if either is NULL
    if (!*lst)             // Special case: the list is currently empty
    {
        *lst = new;         // The new element becomes the first (and last) element
        return ;            // Done: new is now both head and tail
    }
    last = *lst;           // Start at the head of the list
    while (last->next)      // Traverse until we find the element whose next is NULL
        last = last->next;  // Move to the next element; repeat until last->next is NULL
    last->next = new;      // Found the last element: link it to the new element
}                           // new->next is already NULL from ft_lstnew()
```

## Line-by-Line Translation
- `typedef struct s_list` — Define a structure type for list nodes
- `void *content;` — Payload: can point to any type of data
- `struct s_list *next;` — Link to the next node in the list
- `void ft_lstadd_back(t_list **lst, t_list *new)` — Add element to end of list
- `t_list *last;` — Temporary pointer to traverse to the last element
- `if (!lst || !new) return ;` — Guard: need valid pointer-to-list and new element
- `if (!*lst)` — Check if list is currently empty
- `*lst = new; return ;` — Empty list: new element becomes the entire list
- `last = *lst;` — Start at the head
- `while (last->next)` — Loop while current element has a next element
- `last = last->next;` — Advance to the next element
- `last->next = new;` — Found last element: link it to the new element

## Algorithm
1. Check if `lst` and `new` are valid
2. If list is empty (`*lst == NULL`), set `*lst = new` and return
3. Otherwise, traverse to find the last element
4. Set `last->next = new`

## Key Points
- Double pointer `t_list **` to modify caller's pointer
- Handle empty list case first (`*lst == NULL`)
- `new->next` should already be `NULL` from `ft_lstnew`

## Common Traps
- ❌ Forgetting to handle empty list case (`*lst == NULL`)
- ❌ Not setting `new->next` to NULL (should already be NULL from ft_lstnew)

## Related
- [[ft_lstnew]] - Create new element
- [[ft_lstadd_front]] - Add element to front
- [[ft_lstlast]] - Get last element
