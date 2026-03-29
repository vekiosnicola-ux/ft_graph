---
tags: []
date: 2026-03-29
status: complete
---
# Linked Lists

---
tags: [Concepts, blue]
---

## The Problem with Arrays

Arrays are fixed-size blocks of contiguous memory. Inserting in the middle requires shifting elements. Deleting requires shifting. Linked lists solve this.

## The Node Structure

```c
typedef struct s_list
{
    void           *content;      // Data (any type)
    struct s_list  *next;         // Pointer to next node
} t_list;
```

Each node points to the next, forming a chain.

## Memory Layout

```
Array:    [0][1][2][3][4]    <- contiguous, fixed position
    
List:     [data|next] -> [data|next] -> [data|next] -> NULL
              ↑             ↑             ↑
            head          node 2        node 3
```

## ft_lstnew: Creating a Node

From C07 ex00 `ft_lstnew`:

```c
t_list *ft_lstnew(void *content)
{
    t_list *node;
    
    node = malloc(sizeof(t_list));
    if (node == NULL)
        return NULL;
    
    node->content = content;
    node->next = NULL;
    
    return node;
}
```

## ft_lstadd_front: Adding at Head

From C07 ex01 `ft_lstadd_front`:

```c
void ft_lstadd_front(t_list **lst, t_list *new)
{
    new->next = *lst;  // New points to current head
    *lst = new;        // Head is now new node
}
```

## ft_lstsize: Counting Elements

From C07 ex02 `ft_lstsize`:

```c
int ft_lstsize(t_list *lst)
{
    int count;
    
    count = 0;
    while (lst != NULL)  // Until we reach end
    {
        count++;
        lst = lst->next;  // Move to next node
    }
    return count;
}
```

This is the "invisible skeleton" applied to linked structures!

## ft_lstlast: Finding the End

From C07 ex03 `ft_lstlast`:

```c
t_list *ft_lstlast(t_list *lst)
{
    if (lst == NULL)
        return NULL;
    
    while (lst->next != NULL)  // While not at last node
        lst = lst->next;        // Advance
    
    return lst;  // This is the last node
}
```

## ft_lstadd_back: Adding at End

From C07 ex04 `ft_lstadd_back`:

```c
void ft_lstadd_back(t_list **lst, t_list *new)
{
    t_list *last;
    
    if (*lst == NULL)           // Empty list
    {
        *lst = new;              // New is the list
        return;
    }
    
    last = ft_lstlast(*lst);    // Find last node
    last->next = new;           // Connect
}
```

## ft_lstdelone: Freeing One Node

From C07 ex05 `ft_lstdelone`:

```c
void ft_lstdelone(t_list *lst, void (*del)(void *))
{
    if (lst == NULL || del == NULL)
        return;
    
    del(lst->content);  // Free the content using provided function
    free(lst);          // Free the node itself
}
```

## ft_lstclear: Free Entire List

From C07 ex06 `ft_lstclear`:

```c
void ft_lstclear(t_list **lst, void (*del)(void *))
{
    t_list *tmp;
    
    while (*lst != NULL)
    {
        tmp = (*lst)->next;  // Save next before freeing
        ft_lstdelone(*lst, del);
        *lst = tmp;          // Advance
    }
}
```

## ft_lstiter: Applying Function to Each Node

From C07 ex07 `ft_lstiter`:

```c
void ft_lstiter(t_list *lst, void (*f)(void *))
{
    while (lst != NULL)
    {
        f(lst->content);     // Apply function to content
        lst = lst->next;     // Move to next
    }
}
```

## ft_lstmap: Transforming List

From C07 ex08 `ft_lstmap`:

```c
t_list *ft_lstmap(t_list *lst, void *(*f)(void *), void (*del)(void *))
{
    t_list *new_list;
    t_list *current;
    t_list *new_node;
    
    if (lst == NULL || f == NULL)
        return NULL;
    
    new_list = NULL;
    while (lst != NULL)
    {
        new_node = ft_lstnew(f(lst->content));
        if (new_node == NULL)
        {
            ft_lstclear(&new_list, del);
            return NULL;
        }
        ft_lstadd_back(&new_list, new_node);
        lst = lst->next;
    }
    return new_list;
}
```

## Array vs Linked List

| Operation | Array | Linked List |
|-----------|-------|-------------|
| Access by index | O(1) | O(n) |
| Insert at head | O(n) shift | O(1) |
| Insert at tail | O(1) if at end | O(n) or O(1) with tail ptr |
| Delete | O(n) shift | O(1) if node known |
| Memory | Contiguous | Scattered |

## Key Takeaway

Linked lists solve the array insertion/deletion problem by distributing nodes in memory and linking them with pointers. The tradeoff is O(n) access time for O(1) insertions/deletions.

Common operations:
1. Traverse: `while (node != NULL) { node = node->next; }`
2. Insert: Point new node to current head, update head
3. Delete: Save next, free current, advance

---

**Related:** [[pointers]], [[malloc]], [[invisible_skeleton]], [[recursion]]
