---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# btree_level_count

---
tags: [C13, red]
---

## Navigation
← [[btree_apply_suffix|btree_apply_suffix]] | [[btree_level_max|Next: btree_level_max →]]

## What it does
Returns the number of levels in a binary tree. A tree with only a root has 1 level.

## The Insight
Count levels recursively by finding the maximum depth of left and right subtrees. Base case: empty tree has 0 levels, leaf has 1 level.

## Step-by-step Algorithm
1. If node is NULL, return 0.
2. Recursively get the level count of left subtree.
3. Recursively get the level count of right subtree.
4. Return 1 + max(left_levels, right_levels).

## The Code
```c
 "ft_btree.h"  // Header defining t_btree structure

int btree_level_count(t_btree *root)  // Returns the number of levels in the tree
{
    int left;   // Depth (level count) of left subtree
    int right;  // Depth (level count) of right subtree

    if (!root)  // Base case: empty tree has 0 levels
        return (0);  // No nodes means no levels
    left = btree_level_count(root->left);  // Recursively count levels in left subtree
    right = btree_level_count(root->right); // Recursively count levels in right subtree
    if (left > right)  // Compare depths of both subtrees
        return (left + 1);  // Left is deeper: left levels + 1 for current node
    return (right + 1);  // Right is deeper (or equal): right levels + 1 for current node
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 20 | `#include "ft_btree.h"` | Local header with t_btree structure definition |
| 22 | `int btree_level_count(t_btree *root)` | Returns integer count of tree levels |
| 24 | `int left;` | Will hold level count of left subtree |
| 25 | `int right;` | Will hold level count of right subtree |
| 27 | `if (!root)` | Check for empty tree (NULL pointer) |
| 28 | `return (0);` | Empty tree has zero levels |
| 29 | `left = btree_level_count(root->left);` | Recursively get depth of left subtree |
| 30 | `right = btree_level_count(root->right);` | Recursively get depth of right subtree |
| 31 | `if (left > right)` | Compare which subtree is deeper |
| 32 | `return (left + 1);` | Left is deeper: add 1 for current node level |
| 33 | `return (right + 1);` | Right is deeper or equal: add 1 for current node level |

## Common Traps
- ❌ Returning wrong value for NULL tree (should be 0).
- ❌ Forgetting to add 1 for the current node.
- ❌ Not taking the maximum of left and right subtrees.

## Related Concepts
- 01_Concepts/binary_trees|Binary Trees
- 01_Concepts/recursion|Recursion

## Related Exercises
- [[btree_level_max]]
- [[btree_apply_prefix]]
- [[btree_apply_infix]]

How do you count tree levels?
::
```c
if (!root) return 0;
return 1 + max(count(left), count(right));
```
