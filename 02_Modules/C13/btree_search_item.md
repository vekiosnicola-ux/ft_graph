---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# btree_search_item

---
tags: [C13, red]
---

## Navigation
← [[btree_level_max|btree_level_max]] | [[btree_insert_data_level|Next: btree_insert_data_level →]]

## What it does
Searches for an item in a binary search tree using the comparison function. Returns the first matching node's data or NULL if not found.

## The Insight
BST property allows efficient search: compare and go left or right based on comparison result.

## Step-by-step Algorithm
1. If root is NULL, return NULL.
2. Compare item with root->item using cmp function.
3. If equal, return root->item.
4. If item < root->item, search left subtree.
5. If item > root->item, search right subtree.

## The Code
```c
 "ft_btree.h"  // Header defining t_btree structure

void *btree_search_item(t_btree *root, void *data_ref, int (*cmp)(void *, void *))
// Searches BST for data matching data_ref; returns found item or NULL
{
    void *ret;  // Will store result from recursive calls

    if (!root)  // Base case: reached empty subtree (NULL)
        return (NULL);  // Item not found in this path; return NULL
    if ((*cmp)(data_ref, root->item) == 0)  // Compare target with current node
        return (root->item);  // Match found! Return this node's data
    if ((*cmp)(data_ref, root->item) < 0)  // If data_ref < current node's item
        return (btree_search_item(root->left, data_ref, cmp));  // Search LEFT subtree
    // If data_ref > current node's item
    ret = btree_search_item(root->right, data_ref, cmp);  // Search RIGHT subtree
    return (ret);  // Return whatever we found (item or NULL)
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 21 | `#include "ft_btree.h"` | Local header with t_btree structure definition |
| 23 | `void *btree_search_item(...)` | Returns pointer to found item, or NULL if not found |
| 23 | `t_btree *root` | Pointer to current node (or NULL if empty) |
| 23 | `void *data_ref` | The item we're searching for |
| 23 | `int (*cmp)(void *, void *)` | Comparison function: negative if a<b, 0 if equal, positive if a>b |
| 25 | `void *ret;` | Temporary storage for recursive return value |
| 27 | `if (!root)` | Base case: we've reached a NULL leaf (empty spot) |
| 28 | `return (NULL);` | Nothing here; item is not in this branch |
| 29 | `if ((*cmp)(data_ref, root->item) == 0)` | Does current node hold what we're looking for? |
| 30 | `return (root->item);` | Found it! Return the matching data |
| 31 | `if ((*cmp)(data_ref, root->item) < 0)` | Is what we want less than current? |
| 32 | `return (btree_search_item(root->left, ...));` | Go search the left subtree (smaller values) |
| 34 | `ret = btree_search_item(root->right, ...);` | Otherwise, search right subtree (larger values) |
| 35 | `return (ret);` | Return whatever the recursive call returned |

## Common Traps
- ❌ Not checking for NULL root first.
- ❌ Using wrong comparison direction.
- ❌ Not returning the result of recursive calls.

## Related Concepts
- 01_Concepts/binary_trees|Binary Trees
- 01_Concepts/recursion|Recursion

## Related Exercises
- [[btree_insert_data]]
- [[btree_apply_infix]]

How do you search a BST?
::
Compare with root: if equal return, if smaller search left, if larger search right.
