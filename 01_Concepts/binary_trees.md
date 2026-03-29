---
tags: []
date: 2026-03-29
status: complete
---
# Binary Trees

---
tags: [Concepts, blue]
---

## The Concept

A binary tree is a hierarchical structure where each node has at most two children: left and right.

```
        Tree Structure          Node Structure
                                struct s_node
            [root]                  data
           /      \                /      \
        [left]  [right]          *left    *right
        /  \     /   \
      ...  ...  ...  ...
```

## Basic Node Definition

```c
typedef struct s_node
{
    int             data;
    struct s_node   *left;
    struct s_node   *right;
} t_node;
```

## Why Binary Trees?

- **Hierarchical data**: File systems, organization charts, DOM trees
- **Efficient searching**: Binary search trees (BST) enable O(log n) lookup
- **Sorting**: In-order traversal produces sorted sequence
- **Decision trees**: AI/game AI uses binary decision trees

## Binary Search Tree (BST) Property

For every node:
- All left subtree values are **less than** the node
- All right subtree values are **greater than** the node

```
        8
       / \
      3   10
     / \    \
    1   6    14
```

## BST Search

```c
t_node *bst_search(t_node *root, int value)
{
    if (root == NULL)
        return NULL;
    
    if (value == root->data)
        return root;
    else if (value < root->data)
        return bst_search(root->left, value);
    else
        return bst_search(root->right, value);
}
```

Time complexity: O(h) where h is height. Balanced tree: O(log n).

## Tree Traversals

### In-Order (Left, Root, Right)

```c
void inorder(t_node *root)
{
    if (root == NULL)
        return;
    inorder(root->left);
    printf("%d ", root->data);
    inorder(root->right);
}
```

Output for BST above: `1 3 6 8 10 14` (sorted!)

### Pre-Order (Root, Left, Right)

```c
void preorder(t_node *root)
{
    if (root == NULL)
        return;
    printf("%d ", root->data);
    preorder(root->left);
    preorder(root->right);
}
```

Output: `8 3 1 6 10 14`

### Post-Order (Left, Right, Root)

```c
void postorder(t_node *root)
{
    if (root == NULL)
        return;
    postorder(root->left);
    postorder(root->right);
    printf("%d ", root->data);
}
```

Output: `1 6 3 14 10 8`

## Insertion into BST

```c
t_node *bst_insert(t_node *root, int value)
{
    if (root == NULL)
        return ft_node_new(value);
    
    if (value < root->data)
        root->left = bst_insert(root->left, value);
    else if (value > root->data)
        root->right = bst_insert(root->right, value);
    // If equal, do nothing (no duplicates)
    
    return root;
}
```

## Deletion from BST

Three cases:
1. **No children**: Just free the node
2. **One child**: Replace node with its child
3. **Two children**: Find in-order successor (smallest in right subtree), replace, delete successor

## Tree Height

```c
int tree_height(t_node *root)
{
    int left_h;
    int right_h;
    
    if (root == NULL)
        return -1;  // Empty tree has height -1
    
    left_h = tree_height(root->left);
    right_h = tree_height(root->right);
    
    if (left_h > right_h)
        return left_h + 1;
    else
        return right_h + 1;
}
```

## Balance and Performance

```
Balanced (good)              Degenerate (bad)
        O                              O
       / \                            /
      O   O                         O
     / \                            /
    O   O                          O
                                 /
                                O
```

- Balanced: O(log n) search, insert, delete
- Degenerate: O(n) — like a linked list

## Binary Tree vs Linked List

| Structure | Connections | Use Case |
|-----------|-------------|----------|
| Linked List | 1 next | Sequential data |
| Binary Tree | 2 children | Hierarchical, searchable |

Linked list is actually a special case of binary tree where `left = NULL`.

## Key Takeaway

Binary trees organize data hierarchically with O(log n) search (when balanced). Key operations:
1. **Insert/Search**: Navigate left/right based on comparison
2. **Traverse**: Recurse left, process, recurse right
3. **Height**: Recurse both subtrees, return max + 1

The recursive nature mirrors the recursive structure: a tree is either empty or a root with two subtrees.

---

**Related:** [[recursion]], [[linked_lists]], [[pointers]], [[malloc]]
