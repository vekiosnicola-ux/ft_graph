---
tags: [Concepts]
---


# Arrays

## What It Is
An array is a contiguous block of memory containing elements of the same type. The array name acts as a pointer to its first element. Arrays provide O(1) random access but O(n) insertion/deletion. Understanding array memory layout is crucial for pointer arithmetic and efficient algorithms.

## Key Points
- Array name is a constant pointer to first element (cannot be reassigned)
- `arr[i]` is equivalent to `*(arr + i)`
- Contiguous memory: elements are stored side-by-side
- No bounds checking in C (accessing out-of-bounds is undefined behavior)
- Array decay: passing array to function converts to pointer (loses size info)
- 2D arrays are arrays of arrays, stored row-major in memory

## Related Concepts
- [[pointers]]
- pointer_arithmetic
- dynamic_allocation

## Examples
```c
// Basic array declaration and access
int nums[5] = {10, 20, 30, 40, 50};
nums[0] = 10;           // First element
*(nums + 2) = 30;       // Same as nums[2] = 30

// Array as function parameter decays to pointer
int get_length(int *arr) {  // Same as int arr[]
    return sizeof(arr) / sizeof(arr[0]);  // WRONG: size lost!
}

// Pass size separately when passing arrays
int sum_array(int *arr, int size) {
    int sum = 0;
    for (int i = 0; i < size; i++) {
        sum += arr[i];      // or *(arr + i)
    }
    return sum;
}

// 2D array
int matrix[3][4] = {
    {1, 2, 3, 4},
    {5, 6, 7, 8},
    {9, 10, 11, 12}
};
int val = matrix[1][2];  // Row 1, column 2 = 7

// Memory layout (row-major):
// matrix[0]: 1, 2, 3, 4
// matrix[1]: 5, 6, 7, 8
// matrix[2]: 9, 10, 11, 12
// In memory: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12

// Array initialization
int a[10];           // Uninitialized (contains garbage)
int b[10] = {0};     // All zeros
int c[10] = {1, 2};  // First two = 1, 2; rest = 0
int d[] = {1, 2, 3}; // Size inferred = 3
```

## Common Mistakes
- ❌ Array size lost when passed to function (must pass size separately)
- ❌ Out-of-bounds access (C doesn't check, causes undefined behavior)
- ❌ Using `sizeof(arr)` inside function to get element count
- ❌ Trying to assign to array name: `arr = ptr` is illegal
- ❌ Confusing arrays and pointers (arrays are not pointers, though they decay)
