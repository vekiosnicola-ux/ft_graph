---
tags: [C07]
---


# ft_lstsize

## Concept
Counts the number of elements in a linked list.

## Function Signature
```c
int ft_lstsize(t_list *lst);
```

## Parameters
- `lst`: Pointer to the list head

## Return Value
- Number of elements in the list (0 if list is empty)

## Implementation

```c
typedef struct s_list  // Define the list node structure
{
    void *content;          // Pointer to the data stored in this node
    struct s_list *next;    // Pointer to the next node in the list
} t_list;                  // Type alias for struct s_list

// Function: counts and returns the number of elements in the list
int ft_lstsize(t_list *lst)
{
    int count;          // Counter variable to track number of elements

    count = 0;         // Start with zero elements counted
    while (lst)        // Loop while current element is not NULL (end of list)
    {
        count++;        // We've found one more element, increment counter
        lst = lst->next; // Move to the next element in the list
    }                   // Repeat until lst becomes NULL (end of list)
    return (count);     // Return the total number of elements found
}                       // Empty list (lst == NULL) returns 0 (loop never runs)
```

## Line-by-Line Translation
- `typedef struct s_list` — Define a structure type for list nodes
- `void *content;` — Payload: can point to any type of data
- `struct s_list *next;` — Link to the next node in the list
- `int ft_lstsize(t_list *lst)` — Count elements in the linked list
- `int count;` — Variable to store the element count
- `count = 0;` — Initialize counter to zero
- `while (lst)` — Loop while current element is not NULL
- `count++;` — Increment count for each element we visit
- `lst = lst->next;` — Advance to the next element in the list
- `return (count);` — Return the total element count

## Algorithm
1. Initialize a counter to 0
2. Traverse the list using `curr = curr->next`
3. Increment counter for each element
4. Return the counter

## Key Points
- Empty list (`lst == NULL`) returns 0
- Uses `while (lst)` pattern - checks before accessing
- Traversal: `lst = lst->next`

## Common Traps
- ❌ Forgetting to handle NULL list (should return 0)
- ❌ Using `lst->next` before checking if `lst` is NULL

## Related
- [[ft_lstlast]] - Get last element
- [[ft_lstnew]] - Create new element
