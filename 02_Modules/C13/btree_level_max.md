---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# btree_level_max

---
tags: [C13, red]
---

## Navigation
← [[btree_level_count|btree_level_count]] | [[btree_search_item|Next: btree_search_item →]]

## What it does
Returns the maximum number of nodes at any level in the binary tree (the tree's width).

## The Insight
Use level-order traversal (BFS) with a queue to count nodes at each level, tracking the maximum.

## Step-by-step Algorithm
1. If root is NULL, return 0.
2. Use a queue structure to traverse level by level.
3. For each level, count nodes and update maximum.
4. Return the maximum count found.

## The Code
```c
 "ft_btree.h"  // Header defining t_btree structure
 <stdlib.h>    // Provides malloc(), free() for queue management

int btree_level_max(t_btree *root)  // Returns maximum width (nodes at widest level)
{
    t_list *queue;   // Queue for level-order (BFS) traversal
    int max;         // Tracks maximum node count seen at any level
    int level_size;  // Number of nodes at current level being processed

    if (!root)  // Edge case: empty tree has width 0
        return (0);
    max = 1;   // Root alone means at least 1 node at some level
    queue = NULL;  // Initialize empty queue (queue holds t_btree pointers)
    ft_list_push_back(&queue, root);  // Enqueue the root node to start traversal
    while (queue)  // While queue is not empty: process levels one by one
    {
        level_size = ft_list_size(queue);  // Count how many nodes at this level
        if (level_size > max)  // If this level has more nodes than previous max
            max = level_size;   // Update max to new highest count
        while (level_size--)  // Process each node at current level
        {
            root = ft_list_pop_front(&queue);  // Dequeue front node; advance root
            if (root->left)  // If dequeued node has a left child
                ft_list_push_back(&queue, root->left);  // Enqueue left child for next level
            if (root->right)  // If dequeued node has a right child
                ft_list_push_back(&queue, root->right);  // Enqueue right child for next level
        }
    }
    return (max);  // Return the maximum width found
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 23 | `int btree_level_max(t_btree *root)` | Returns integer: maximum nodes at any single level |
| 27 | `t_list *queue;` | Queue implemented as linked list for BFS traversal |
| 31 | `if (!root)` | Check for empty tree input |
| 32 | `return (0);` | Empty tree has zero width |
| 33 | `max = 1;` | Start with at least 1 (the root node) |
| 34 | `queue = NULL;` | Initialize empty queue (no nodes queued yet) |
| 35 | `ft_list_push_back(&queue, root);` | Add root to queue to begin traversal |
| 36 | `while (queue)` | Loop while queue has nodes to process |
| 38 | `level_size = ft_list_size(queue);` | Count nodes at current level |
| 39-40 | (max update) | Track the largest level_size seen |
| 41 | `while (level_size--)` | Process all nodes at this level one by one |
| 42 | `root = ft_list_pop_front(&queue);` | Remove and get next node from queue front |
| 43-44 | (queue children) | If node has left/right child, add to queue for next level |

## Common Traps
- ❌ Not handling empty tree (NULL root).
- ❌ Forgetting to count all nodes at current level before processing next.
- ❌ Not using a queue or similar structure for level-order traversal.

## Related Concepts
- 01_Concepts/binary_trees|Binary Trees
- 01_Concepts/linked_lists|Linked Lists
- 01_Concepts/recursion|Recursion

## Related Exercises
- [[btree_level_count]]
- [[btree_insert_data_level]]

How do you find max width of a tree?
::
Use BFS with queue, count nodes at each level, track maximum.
