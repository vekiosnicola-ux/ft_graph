---
tags: [C07]
---


# ft_lstmap

## Concept
Creates a new list by applying function `f` to the content of each element. Uses `del` to free memory if allocation fails.

## Function Signature
```c
t_list *ft_lstmap(t_list *lst, void *(*f)(void *), void (*del)(void *));
```

## Parameters
- `lst`: Pointer to the list head
- `f`: Function to apply to each element's content
- `del`: Function to free memory if allocation fails

## Return Value
- Pointer to the new list
- `NULL` if allocation fails or if `lst`/`f` is `NULL`

## Implementation

```c
 <stdlib.h> // Provides malloc() for dynamic memory allocation

typedef struct s_list  // Define the list node structure
{
    void *content;          // Pointer to the data stored in this node
    struct s_list *next;    // Pointer to the next node in the list
} t_list;                  // Type alias for struct s_list

// Function: creates a new list by applying f() to each element's content
// Returns the new list, or NULL if allocation fails
t_list *ft_lstmap(t_list *lst, void *(*f)(void *), void (*del)(void *))
{
    t_list *new_list;      // Pointer to the first element of new list
    t_list *new_elem;      // Temporary pointer for creating new elements
    t_list *last;          // Tracks the last element (for linking)

    if (!lst || !f)        // Guard: check for NULL list or NULL function
        return (NULL);      // Cannot proceed without both
    new_list = ft_lstnew(f(lst->content)); // Create first element: apply f to content
    if (!new_list)         // Check if first allocation failed
        return (NULL);      // Propagate NULL error
    last = new_list;       // 'last' now points to first element
    lst = lst->next;       // Move to second element of original list
    while (lst)            // Loop through remaining elements of original list
    {
        new_elem = ft_lstnew(f(lst->content)); // Create new element with transformed content
        if (!new_elem)         // If allocation failed for this element
        {
            ft_lstclear(&new_list, del); // Clean up: free entire new list
            return (NULL);       // Return NULL to indicate failure
        }
        last->next = new_elem;  // Link the previous element to this new element
        last = new_elem;        // Update 'last' to be this new element
        lst = lst->next;        // Move to next element in original list
    }                           // Repeat until all original elements are processed
    return (new_list);         // Return the head of the newly created list
}
```

## Line-by-Line Translation
- `#include <stdlib.h>` — Header for malloc() and free()
- `typedef struct s_list` — Define a structure type for list nodes
- `void *content;` — Payload: can point to any type of data
- `struct s_list *next;` — Link to the next node in the list
- `t_list *ft_lstmap(...)` — Create new list by applying function to each element
- `if (!lst || !f) return (NULL);` — Guard against NULL inputs
- `new_list = ft_lstnew(f(lst->content));` — Create first element with transformed content
- `if (!new_list) return (NULL);` — Check for malloc failure
- `last = new_list;` — Track the last element for linking
- `lst = lst->next;` — Advance to second element
- `while (lst)` — Loop through remaining elements
- `new_elem = ft_lstnew(f(lst->content));` — Transform content and create new element
- `if (!new_elem)` — Check for allocation failure
- `ft_lstclear(&new_list, del);` — Clean up previously allocated elements
- `return (NULL);` — Propagate failure
- `last->next = new_elem;` — Link previous element to new one
- `last = new_elem;` — Update last pointer
- `lst = lst->next;` — Move to next original element
- `return (new_list);` — Return the new list

## Algorithm
1. Check if `lst` and `f` are valid
2. Create first element: `ft_lstnew(f(lst->content))`
3. If allocation fails, return `NULL`
4. Traverse original list, creating new elements
5. If any allocation fails, clear new list and return `NULL`
6. Link new elements properly
7. Return the new list

## Key Points
- Combines `ft_lstnew` + `ft_lstclear` for error handling
- Uses `ft_lstadd_back` logic manually (tracking `last`)
- Must handle allocation failure at each step

## Common Traps
- ❌ Forgetting to handle allocation failure and clean up
- ❌ Not properly linking new elements
- ❌ Forgetting to clear the list if `del` fails midway

## Related
- [[ft_lstiter]] - Traverse without creating
- [[ft_lstnew]] - Create new element
- [[ft_lstclear]] - Free entire list
