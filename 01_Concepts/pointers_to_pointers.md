---
tags: [Concepts]
---


# Pointers to Pointers

## What It Is
A pointer to a pointer is a variable that stores the address of another pointer. This creates a chain of indirection: `ptr_to_ptr -> ptr -> value`. Useful when you need to modify the pointer itself (not just what it points to) from within a function.

## Key Points
- Declaration: `int **ptr` (pointer to pointer to int)
- First dereference gets the inner pointer, second gets the value
- Enables modifying pointer values from functions (e.g., pointer arguments that change)
- Common in 2D arrays, dynamic array of strings, and linked list operations
- Chain of indirection: `**ptr` gives the final value

## Related Concepts
- [[pointers]]
- [[multi_level_pointers]]
- dynamic_allocation

## Examples
```c
// Modifying a pointer via double indirection
void allocate_int(int **ptr, int value) {
    *ptr = malloc(sizeof(int));
    **ptr = value;
}

int main(void) {
    int *p = NULL;
    allocate_int(&p, 42);  // p now points to memory containing 42
    free(p);
    return 0;
}

// Swapping two pointers
void swap_ptrs(char **a, char **b) {
    char *temp = *a;
    *a = *b;
    *b = temp;
}

int main(void) {
    char *s1 = "hello";
    char *s2 = "world";
    swap_ptrs(&s1, &s2);  // s1="world", s2="hello"
    return 0;
}

// 2D array access
int grid[3][3] = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
int *row = grid[1];        // row points to 4
int **ptr_to_row = &row;  // pointer to pointer to access row
```

## Common Mistakes
- ❌ Forgetting to dereference when assigning: `*ptr = &value`, not `ptr = &value`
- ❌ Losing the original pointer (memory leak) when reassigning inside functions
- ❌ Confusing the level of indirection (using `*ptr` when should use `**ptr`)
