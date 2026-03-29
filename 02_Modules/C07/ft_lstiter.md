---
tags: [C07]
---


# ft_lstiter

## Concept
Applies a function `f` to the content of each element in the list (traversal).

## Function Signature
```c
void ft_lstiter(t_list *lst, void (*f)(void *));
```

## Parameters
- `lst`: Pointer to the list head
- `f`: Function pointer to apply to each element's content

## Return Value
- `void`

## Implementation

```c
typedef struct s_list  // Define the list node structure
{
    void *content;          // Pointer to the data stored in this node
    struct s_list *next;    // Pointer to the next node in the list
} t_list;                  // Type alias for struct s_list

// Function: applies function f to the content of every element in the list
void ft_lstiter(t_list *lst, void (*f)(void *))
{
    if (!lst || !f)         // Guard: check for NULL list or NULL function pointer
        return ;            // Nothing to iterate if either is NULL
    while (lst)             // Loop through each element until we reach the end
    {                       // (NULL marks the end of the list)
        f(lst->content);    // Apply function f to this element's content
        lst = lst->next;    // Move to the next element in the list
    }                       // Loop continues until lst becomes NULL (end reached)
}                           // Function f is called once per element, in order
```

## Line-by-Line Translation
- `typedef struct s_list` — Define a structure type for list nodes
- `void *content;` — Payload: can point to any type of data
- `struct s_list *next;` — Link to the next node in the list
- `void ft_lstiter(t_list *lst, void (*f)(void *))` — Iterate and apply function to each element
- `if (!lst || !f) return ;` — Guard: exit early if list or function is NULL
- `while (lst)` — Loop while we haven't reached the end (NULL)
- `f(lst->content);` — Apply function f to the current element's content
- `lst = lst->next;` — Advance to the next element in the list

## Algorithm
1. Check if `lst` and `f` are valid
2. Traverse the list from head to tail
3. For each element, call `f(lst->content)`

## Key Points
- Does not modify the list, only reads/applies function
- Does not allocate or free memory
- Simple traversal pattern: `while (lst)`

## Common Traps
- ❌ Forgetting to check if `lst` or `f` is NULL
- ❌ Modifying `lst` directly if you need to preserve the list

## Related
- [[ft_lstmap]] - Apply function and create new list
- [[ft_lstiter]] - Traverse and apply function
