---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# btree_create_node

---
tags: [C13, red]
---

## Navigation
← [[C11_Index|C13 INDEX]] | [[btree_insert_data|Next: btree_insert_data →]]

## What it does
Creates a new node for a binary tree with the given item as data. Both left and right child pointers are initialized to NULL.

## The Insight
A binary tree node contains data and two pointers (left and right). Using `malloc` allocates memory for the node structure.

## Step-by-step Algorithm
1. Include necessary headers (`stdlib.h` for malloc).
2. Allocate memory for a node using `malloc(sizeof(t_btree))`.
3. Set the node's `item` to the parameter value.
4. Set `left` and `right` to NULL.
5. Return the newly created node.

## The Code
```c
 <stdlib.h>   // Provides malloc() for dynamic memory allocation
 "ft_btree.h"  // Header defining t_btree structure

t_btree *btree_create_node(void *item)  // Creates and returns a new binary tree node
{
    t_btree *node;  // Pointer to the newly allocated node

    node = malloc(sizeof(t_btree));  // Request memory for one t_btree structure
    if (!node)  // Check if malloc failed (returns NULL when system has no memory)
        return (NULL);  // Signal allocation failure to caller
    node->item = item;  // Store the provided item (data) in this node
    node->left = NULL;  // New node has no left child
    node->right = NULL;  // New node has no right child
    return (node);  // Return pointer to the newly created node
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 21 | `#include <stdlib.h>` | Header for malloc() and free() |
| 22 | `#include "ft_btree.h"` | Local header defining t_btree structure |
| 24 | `t_btree *btree_create_node(void *item)` | Creates one tree node; item is generic pointer |
| 26 | `t_btree *node;` | Variable to hold pointer to newly allocated node |
| 28 | `node = malloc(sizeof(t_btree));` | Allocate bytes for exactly one t_btree structure |
| 29 | `if (!node)` | Check if malloc failed (NULL means out of memory) |
| 30 | `return (NULL);` | Tell caller allocation failed |
| 31 | `node->item = item;` | Store the item/data in this node |
| 32 | `node->left = NULL;` | Initialize left child pointer to NULL (no subtree) |
| 33 | `node->right = NULL;` | Initialize right child pointer to NULL (no subtree) |
| 34 | `return (node);` | Return the new node to the caller |

## Common Traps
- ❌ Forgetting to include `stdlib.h` for malloc.
- ❌ Not checking if malloc failed (returned NULL).
- ❌ Forgetting to initialize left and right to NULL.
- ❌ Using sizeof on the wrong type.

## Related Concepts
- 01_Concepts/binary_trees|Binary Trees
- 01_Concepts/malloc|malloc/free
- 01_Concepts/recursion|Recursion

## Related Exercises
- [[btree_insert_data]]
- [[btree_apply_prefix]]
- [[btree_apply_infix]]
- [[btree_apply_suffix]]

How do you create a binary tree node?
::
```c
t_btree *node = malloc(sizeof(t_btree));
node->item = item;
node->left = NULL;
node->right = NULL;
return (node);
```
