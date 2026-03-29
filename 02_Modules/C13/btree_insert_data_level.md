---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# btree_insert_data_level

---
tags: [C13, red]
---

## Navigation
← [[btree_search_item|btree_search_item]] | [[C11_Index|C13 INDEX →]]

## What it does
Inserts a new node with the given item into a binary tree using level-order traversal (breadth-first). Finds the first empty position at the shallowest level.

## The Insight
Level-order insertion ensures the tree remains balanced. Use a queue to traverse level by level and insert at first available child position.

## Step-by-step Algorithm
1. If root is NULL, create and return new node.
2. Use a queue for level-order traversal.
3. For each node, check if left child is NULL: if so, insert there.
4. If left is not NULL but right is NULL, insert at right child.
5. If both children exist, enqueue them and continue.
6. Return root.

## The Code
```c
 "ft_btree.h"  // Header defining t_btree structure
 <stdlib.h>    // Provides malloc(), free() for queue management

void btree_insert_data_level(t_btree **root, void *item, int (*cmp)(void *, void *))
// Inserts item at shallowest (level-order) position; cmp parameter unused in this implementation
{
    t_list *queue;   // Queue for level-order (BFS) traversal
    t_btree *node;   // Current node being examined from queue

    if (!*root)  // If tree is completely empty (NULL root pointer)
    {
        *root = btree_create_node(item);  // Create first node as the root
        return;  // Done! Exit immediately
    }
    queue = NULL;  // Initialize empty queue
    ft_list_push_back(&queue, *root);  // Start by examining the root node
    while (queue)  // While there are nodes to examine in the queue
    {
        node = ft_list_pop_front(&queue);  // Get next node from front of queue
        if (!node->left)  // If this node has NO left child
        {
            node->left = btree_create_node(item);  // Insert new node as left child
            break;  // Insertion complete; exit the traversal loop
        }
        else  // Left child exists; queue it for later examination
            ft_list_push_back(&queue, node->left);  // Will examine this subtree later
        if (!node->right)  // If this node has NO right child
        {
            node->right = btree_create_node(item);  // Insert new node as right child
            break;  // Insertion complete; exit the traversal loop
        }
        else  // Right child exists; queue it for later examination
            ft_list_push_back(&queue, node->right);  // Will examine this subtree later
    }
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 25 | `void btree_insert_data_level(...)` | Returns nothing; modifies tree via pointer-to-pointer |
| 30 | `t_list *queue;` | Queue implemented as linked list for BFS |
| 31 | `t_btree *node;` | Will point to node being currently examined |
| 33 | `if (!*root)` | Check if tree is completely empty |
| 35 | `*root = btree_create_node(item);` | Create and set as new root node |
| 36 | `return;` | Tree was empty; insertion done |
| 38 | `queue = NULL;` | Initialize empty queue |
| 39 | `ft_list_push_back(&queue, *root);` | Enqueue root to begin level-order traversal |
| 40 | `while (queue)` | Loop while queue has nodes to process |
| 41 | `node = ft_list_pop_front(&queue);` | Dequeue front node for examination |
| 43 | `if (!node->left)` | Does this node lack a left child? |
| 44 | `node->left = btree_create_node(item);` | Insert new node as left child |
| 45 | `break;` | Found spot at shallowest level; stop searching |
| 47 | `ft_list_push_back(&queue, node->left);` | Left child exists; add to queue for later |
| 49 | `if (!node->right)` | Does this node lack a right child? |
| 50 | `node->right = btree_create_node(item);` | Insert new node as right child |
| 52 | `break;` | Found spot at shallowest level; stop searching |
| 54 | `ft_list_push_back(&queue, node->right);` | Right child exists; add to queue for later |

## Common Traps
- ❌ Not handling empty tree (create first node).
- ❌ Not using level-order traversal (must insert at shallowest level).
- ❌ Forgetting to use a queue for BFS.
- ❌ Breaking after inserting instead of continuing to free queue.

## Related Concepts
- 01_Concepts/binary_trees|Binary Trees
- 01_Concepts/linked_lists|Linked Lists
- 01_Concepts/recursion|Recursion

## Related Exercises
- [[btree_insert_data]]
- [[btree_level_max]]
- [[btree_create_node]]

How do you insert at the shallowest level?
::
Use BFS with queue. Insert at first NULL child found.
