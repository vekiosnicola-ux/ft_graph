---
tags: [C07]
---


# ft_lstnew

## Concept
Creates a new list element by allocating memory and initializing its fields.

## Function Signature
```c
t_list *ft_lstnew(void *content);
```

## Parameters
- `content`: The content to store in the new element

## Return Value
- Returns the new element
- Returns `NULL` if malloc fails

## Implementation

```c
 <stdlib.h> // Provides malloc() and free() for dynamic memory allocation

typedef struct s_list  // Define the list node structure
{
    void *content;          // Pointer to the data stored in this node
    struct s_list *next;    // Pointer to the next node in the list
} t_list;                  // Type alias for struct s_list

// Function: creates and returns a brand new list element
t_list *ft_lstnew(void *content)
{
    t_list *element;       // Pointer to the newly allocated element

    element = malloc(sizeof(t_list)); // Step 1: Allocate memory for one node
    if (!element)          // Step 2: Check if malloc() failed (returns NULL)
        return (NULL);      // Return NULL to indicate allocation failure
    element->content = content; // Step 3: Store the provided content in the node
    element->next = NULL;     // Step 4: Initialize next pointer to NULL
    return (element);         // Step 5: Return the newly created element
}                              // The caller is responsible for linking it to a list
```

## Line-by-Line Translation
- `#include <stdlib.h>` — Header for malloc() and free()
- `typedef struct s_list` — Define a structure type for list nodes
- `void *content;` — Payload: can point to any type of data (generic pointer)
- `struct s_list *next;` — Link to the next node in the list (NULL if last)
- `t_list *ft_lstnew(void *content)` — Create a new list element
- `element = malloc(sizeof(t_list));` — Allocate enough bytes for one t_list structure
- `if (!element) return (NULL);` — Check if allocation failed
- `element->content = content;` — Store the provided content in the new node
- `element->next = NULL;` — Initialize next pointer (important: this is the end marker)
- `return (element);` — Return the newly created element to the caller

## Algorithm
1. Allocate memory for the new element using `malloc`
2. If allocation fails, return `NULL`
3. Set `element->content` to the parameter `content`
4. Set `element->next` to `NULL`
5. Return the new element

## Key Points
- `t_list` structure holds `void *content` for flexibility
- Always initialize `next` to `NULL`
- Must check `malloc` return value

## Common Traps
- ❌ Forgetting to check malloc return value
- ❌ Not initializing `next` to NULL
- ❌ Incorrect sizeof usage

## Related
- [[ft_lstadd_front]] - Add element to front
- [[ft_lstadd_back]] - Add element to back
- [[ft_lstclear]] - Free entire list
