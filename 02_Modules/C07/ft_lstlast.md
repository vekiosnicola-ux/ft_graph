---
tags: [C07]
---


# ft_lstlast

## Concept
Returns a pointer to the last element of a linked list.

## Function Signature
```c
t_list *ft_lstlast(t_list *lst);
```

## Parameters
- `lst`: Pointer to the list head

## Return Value
- Pointer to the last element
- `NULL` if list is empty

## Implementation

```c
typedef struct s_list  // Define the list node structure
{
    void *content;          // Pointer to the data stored in this node
    struct s_list *next;    // Pointer to the next node in the list
} t_list;                  // Type alias for struct s_list

// Function: returns a pointer to the LAST element in the list
t_list *ft_lstlast(t_list *lst)
{
    if (!lst)              // Guard: check if list is NULL (empty)
        return (NULL);      // Cannot get last element from empty list
    while (lst->next)      // Loop while current element has a 'next' element
        lst = lst->next;    // Move to the next element; repeat until next is NULL
    return (lst);           // When next is NULL, current element IS the last one
}                           // Return pointer to the final element
```

## Line-by-Line Translation
- `typedef struct s_list` — Define a structure type for list nodes
- `void *content;` — Payload: can point to any type of data
- `struct s_list *next;` — Link to the next node in the list
- `t_list *ft_lstlast(t_list *lst)` — Find and return the last element
- `if (!lst) return (NULL);` — Guard: empty list has no last element
- `while (lst->next)` — Loop while current element has a next element
- `lst = lst->next;` — Advance to the next element in the list
- `return (lst);` — Return the last element (the one with next == NULL)

## Algorithm
1. If `lst` is NULL, return NULL
2. Traverse the list until `curr->next` is NULL
3. Return the current element (which is the last)

## Key Points
- Empty list returns `NULL`
- Loop condition `while (lst->next)` stops at last element
- Last element has `next == NULL`

## Common Traps
- ❌ Forgetting to check if `lst` is NULL at the start
- ❌ Returning `lst->next` instead of `lst` when it's the last element

## Related
- [[ft_lstsize]] - Count elements
- [[ft_lstadd_back]] - Add element to end
