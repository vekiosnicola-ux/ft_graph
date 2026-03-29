---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# btree_apply_infix

---
tags: [C13, red]
---

## Navigation
← [[btree_apply_prefix|btree_apply_prefix]] | [[btree_apply_suffix|Next: btree_apply_suffix →]]

## What it does
Applies a given function to each node in the tree using infix traversal (left -> root -> right). For BSTs, this processes nodes in ascending order.

## The Insight
Infix traversal processes left subtree, then root, then right. For binary search trees, this gives sorted order.

## Step-by-step Algorithm
1. If node is NULL, return.
2. Recursively call on node->left.
3. Apply the function to node->item.
4. Recursively call on node->right.

## The Code
```c
 "ft_btree.h"  // Header defining t_btree structure

void btree_apply_infix(t_btree *root, void (*applyf)(void *))
// Applies applyf to every node in infix order: left, then root, then right
{
    if (!root)  // Base case: empty tree (NULL pointer)
        return;  // Nothing to do; exit immediately
    btree_apply_infix(root->left, applyf);  // RECURSE LEFT: process entire left subtree first
    applyf(root->item);  // PROCESS ROOT IN THE MIDDLE: apply function to current node
    btree_apply_infix(root->right, applyf); // RECURSE RIGHT: process entire right subtree last
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 20 | `#include "ft_btree.h"` | Local header with t_btree structure definition |
| 22 | `void btree_apply_infix(...)` | Visits left, then root, then right; returns nothing |
| 22 | `t_btree *root` | Pointer to current node in tree (or NULL if empty) |
| 22 | `void (*applyf)(void *)` | Function pointer: takes void*, returns void |
| 24 | `if (!root)` | Check if current node is NULL (empty subtree) |
| 25 | `return;` | Base case: nothing to process; go back up the recursion |
| 26 | `btree_apply_infix(root->left, applyf);` | INFIX: Process left subtree completely BEFORE root |
| 27 | `applyf(root->item);` | INFIX: Process current node's data BETWEEN left and right |
| 28 | `btree_apply_infix(root->right, applyf);` | INFIX: Process right subtree completely AFTER root |

## Common Traps
- ❌ Not checking for NULL before accessing node.
- ❌ Forgetting to recurse on left before processing root.
- ❌ Wrong order of operations (root must be between left and right).

## Related Concepts
- 01_Concepts/binary_trees|Binary Trees
- 01_Concepts/recursion|Recursion

## Related Exercises
- [[btree_apply_prefix]]
- [[btree_apply_suffix]]
- [[btree_search_item]]

What is infix traversal order?
::
Left → Root → Right (gives sorted order for BST!)
