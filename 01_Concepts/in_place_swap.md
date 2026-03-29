---
tags: [Concepts]
---


# In-Place Swap

## What It Is
Swapping values without using a temporary variable. Possible through arithmetic operations (addition/subtraction or XOR) or through simultaneous assignment. Essential for sorting algorithms and any situation where you need to exchange two values using only the storage locations of those values.

## Key Points
- **Temporary variable method**: most readable, always works
- **Addition/subtraction**: `a = a + b; b = a - b; a = a - b;` (risk of overflow)
- **XOR method**: `a ^= b; b ^= a; a ^= b;` (works for integers, no overflow risk)
- **Simultaneous assignment**: C can assign multiple variables at once: `a = a + b - (b = a)`
- In C, simple swap with temp is clearest and most reliable

## Related Concepts
- [[ft_swap]]
- [[in_place_swap]]
- bitwise_operations

## Examples
```c
// Standard swap with temporary variable
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// XOR swap (no temporary variable, no overflow)
void xor_swap(int *a, int *b) {
    if (a == b) return;  // same address, no swap needed
    *a ^= *b;
    *b ^= *a;
    *a ^= *b;
}

// Addition/subtraction swap (risks overflow for large values)
void add_swap(int *a, int *b) {
    *a = *a + *b;
    *b = *a - *b;
    *a = *a - *b;
}

// Swap using simultaneous assignment (C syntax quirk)
void simultaneous_swap(int *a, int *b) {
    *a = *a + *b - (*b = *a);
    // After: b gets old a, then a gets (old a + old b - old a) = old b
}
```

## Common Mistakes
- ❌ Swapping without pointers when values are in functions (swaps local copies only)
- ❌ XOR swap with same pointer (a ^= a sets to 0)
- ❌ Addition swap with large numbers causing integer overflow
- ❌ Forgetting that swap requires dereferencing for pointer parameters
