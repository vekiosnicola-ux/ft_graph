---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# btree_apply_suffix

---
tags: [C13, red]
---

## Navigation
← [[btree_apply_infix|btree_apply_infix]] | [[btree_level_count|Next: btree_level_count →]]

## What it does
Applies a given function to each node in the tree using suffix/postfix traversal (left -> right -> root).

## The Insight
Suffix traversal processes children before the root. Useful for cleanup operations where you free children before the parent.

## Step-by-step Algorithm
1. If node is NULL, return.
2. Recursively call on node->left.
3. Recursively call on node->right.
4. Apply the function to node->item.

## The Code
```c
 "ft_btree.h"  // Header defining t_btree structure

void btree_apply_suffix(t_btree *root, void (*applyf)(void *))
// Applies applyf to every node in suffix order: left, then right, then root
{
    if (!root)  // Base case: empty tree (NULL pointer)
        return;  // Nothing to do; exit immediately
    btree_apply_suffix(root->left, applyf);  // RECURSE LEFT: process entire left subtree first
    btree_apply_suffix(root->right, applyf); // RECURSE RIGHT: process entire right subtree second
    applyf(root->item);  // PROCESS ROOT LAST: apply function to current node after children
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 20 | `#include "ft_btree.h"` | Local header with t_btree structure definition |
| 22 | `void btree_apply_suffix(...)` | Visits children before root; returns nothing |
| 22 | `t_btree *root` | Pointer to current node in tree (or NULL if empty) |
| 22 | `void (*applyf)(void *)` | Function pointer: takes void*, returns void |
| 24 | `if (!root)` | Check if current node is NULL (empty subtree) |
| 25 | `return;` | Base case: nothing to process; go back up the recursion |
| 26 | `btree_apply_suffix(root->left, applyf);` | SUFFIX: Process entire left subtree BEFORE current node |
| 27 | `btree_apply_suffix(root->right, applyf);` | SUFFIX: Process entire right subtree BEFORE current node |
| 28 | `applyf(root->item);` | SUFFIX: Process current node AFTER both subtrees (last!) |

## Common Traps
- ❌ Not checking for NULL before accessing node.
- ❌ Processing root before children (must be last in suffix).
- ❌ Forgetting to recurse on both children.

## Related Concepts
- 01_Concepts/binary_trees|Binary Trees
- 01_Concepts/recursion|Recursion

## Related Exercises
- [[btree_apply_prefix]]
- [[btree_apply_infix]]
- [[btree_level_count]]

What is suffix traversal order?
::
Left → Right → Root (useful for freeing memory)
