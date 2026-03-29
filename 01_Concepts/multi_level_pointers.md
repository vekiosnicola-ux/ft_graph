---
tags: [Concepts]
---


# Multi-Level Pointers

## What It Is
Multi-level pointers involve three or more levels of indirection (e.g., `int ***ptr`). Each asterisk adds another layer of dereferencing. The extreme case is the 9-star exercise (`int *********nbr`) where you must dereference all nine levels to set the final value to 42.

## Key Points
- Triple pointer (`***`): pointer to pointer to pointer
- Each level of indirection requires one more dereference (`*`) to reach the value
- Used for complex data structures (trees, nested linked lists), modifying pointer arrays
- The 9-star exercise requires exactly nine asterisks in the parameter and nine dereferences
- More asterisks = deeper chain of indirection

## Related Concepts
- [[pointers_to_pointers]]
- [[pointers]]
- [[ft_ultimate_ft]]

## Examples
```c
// Triple pointer - modify array of pointers
void alloc_strings(char ***arr, int count) {
    *arr = malloc(count * sizeof(char *));
    for (int i = 0; i < count; i++) {
        (*arr)[i] = malloc(50);
    }
}

int main(void) {
    char **strings = NULL;
    alloc_strings(&strings, 5);  // strings now allocated
    free_strings(&strings, 5);
    return 0;
}

// Nine-star exercise (ft_ultimate_ft from C01)
void ft_ultimate_ft(int *********nbr) {
    *********nbr = 42;
}

// Usage would be:
int main(void) {
    int value;
    int *p1 = &value;
    int **p2 = &p1;
    int ***p3 = &p2;
    int ****p4 = &p3;
    int *****p5 = &p4;
    int ******p6 = &p5;
    int *******p7 = &p6;
    int ********p8 = &p7;
    int *********p9 = &p8;
    ft_ultimate_ft(p9);  // value is now 42
    return 0;
}
```

## Common Mistakes
- ❌ Counting the wrong number of asterisks (must be exactly 9 for 9-star exercise)
- ❌ Forgetting to dereference at each level when assigning
- ❌ Not understanding that each `*` on the parameter type is a level of indirection
