---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# btree_insert_data

---
tags: [C13, red]
---

## Navigation
← [[btree_create_node|btree_create_node]] | [[btree_apply_prefix|Next: btree_apply_prefix →]]

## What it does
Inserts a new node with the given item into a binary search tree (BST). Compares items using the comparison function to maintain BST property (left < parent < right).

## The Insight
Binary search trees maintain ordering: smaller values go left, larger values go right. Recursively traverse to find the correct insertion point.

## Step-by-step Algorithm
1. If root is NULL, create and return a new node.
2. If item < root->item (using cmp function), insert into left subtree.
3. If item >= root->item, insert into right subtree.
4. Return root.

## The Code
```c
 "ft_btree.h"  // Header defining t_btree structure and function signatures

void btree_insert_data(t_btree **root, void *item, int (*cmp)(void *, void *))
// Inserts item into BST rooted at *root; cmp compares two items
{
    if (!*root)  // If current position is empty (NULL pointer)
    {
        *root = btree_create_node(item);  // Create and insert new node here
        return;  // Insertion complete; exit function
    }
    // Compare new item with current node's item to decide where to go
    if ((*cmp)(item, (*root)->item) < 0)  // If new item < current node's item
        btree_insert_data(&(*root)->left, item, cmp);  // Recurse into left subtree
    else  // New item >= current node's item
        btree_insert_data(&(*root)->right, item, cmp);  // Recurse into right subtree
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 20 | `#include "ft_btree.h"` | Local header with t_btree definition |
| 22 | `void btree_insert_data(...)` | Returns nothing; modifies tree via pointer-to-pointer |
| 22 | `t_btree **root` | Pointer to pointer: allows modifying caller's root pointer |
| 22 | `int (*cmp)(void *, void *)` | Comparison function: returns - if a<b, 0 if a==b, + if a>b |
| 24 | `if (!*root)` | If the pointer at this position is NULL (empty spot) |
| 26 | `*root = btree_create_node(item);` | Create new node and store its address at this position |
| 27 | `return;` | Done! Exit without recursing further |
| 29 | `if ((*cmp)(item, (*root)->item) < 0)` | Call comparison function: is new item less than current? |
| 30 | `btree_insert_data(&(*root)->left, item, cmp);` | Recurse left: pass address of left child pointer |
| 32 | `btree_insert_data(&(*root)->right, item, cmp);` | Recurse right: pass address of right child pointer |

## Common Traps
- ❌ Not handling NULL root (must create first node).
- ❌ Forgetting to dereference root pointer correctly.
- ❌ Using wrong comparison direction (must match BST invariant).
- ❌ Not passing address of child pointers when recursing.

## Related Concepts
- 01_Concepts/binary_trees|Binary Trees
- 01_Concepts/recursion|Recursion
- 01_Concepts/functionPointers|Function Pointers

## Related Exercises
- [[btree_create_node]]
- [[btree_search_item]]
- [[btree_apply_infix]]

How do you insert into a BST?
::
Compare item with root: if smaller go left, if larger go right. Recurse until NULL, then create node.
