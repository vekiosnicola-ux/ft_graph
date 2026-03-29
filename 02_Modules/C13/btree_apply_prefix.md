---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# btree_apply_prefix

---
tags: [C13, red]
---

## Navigation
← [[btree_insert_data|btree_insert_data]] | [[btree_apply_infix|Next: btree_apply_infix →]]

## What it does
Applies a given function to each node in the tree using prefix traversal (root -> left -> right).

## The Insight
Prefix traversal processes the root before its children. Recursively apply the function to root, then recurse left, then right.

## Step-by-step Algorithm
1. If node is NULL, return.
2. Apply the function to node->item.
3. Recursively call on node->left.
4. Recursively call on node->right.

## The Code
```c
 "ft_btree.h"  // Header defining t_btree structure

void btree_apply_prefix(t_btree *root, void (*applyf)(void *))
// Applies applyf to every node in prefix order: root, then left, then right
{
    if (!root)  // Base case: empty tree (NULL pointer)
        return;  // Nothing to do; exit immediately
    applyf(root->item);  // PROCESS ROOT FIRST: apply function to current node
    btree_apply_prefix(root->left, applyf);  // RECURSE LEFT: traverse entire left subtree
    btree_apply_prefix(root->right, applyf); // RECURSE RIGHT: traverse entire right subtree
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 20 | `#include "ft_btree.h"` | Local header with t_btree structure definition |
| 22 | `void btree_apply_prefix(...)` | Visits root before children; returns nothing |
| 22 | `t_btree *root` | Pointer to current node in tree (or NULL if empty) |
| 22 | `void (*applyf)(void *)` | Function pointer: takes void*, returns void |
| 24 | `if (!root)` | Check if current node is NULL (empty subtree) |
| 25 | `return;` | Base case: nothing to process; go back up the recursion |
| 26 | `applyf(root->item);` | PREFIX: Process current node's data before children |
| 27 | `btree_apply_prefix(root->left, applyf);` | Recursively process entire left subtree |
| 28 | `btree_apply_prefix(root->right, applyf);` | Recursively process entire right subtree |

## Common Traps
- ❌ Not checking for NULL before accessing node.
- ❌ Forgetting to recurse on both children.
- ❌ Applying function to wrong node (must be root first in prefix).

## Related Concepts
- 01_Concepts/binary_trees|Binary Trees
- 01_Concepts/recursion|Recursion

## Related Exercises
- [[btree_apply_infix]]
- [[btree_apply_suffix]]
- [[btree_insert_data]]

What is prefix traversal order?
::
Root → Left → Right (process root first)
