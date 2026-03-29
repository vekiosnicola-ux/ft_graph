---
tags: [Concepts]
---


# Function Pointers

## What It Is
A function pointer is a variable that stores the memory address of a function rather than data. In C, functions occupy memory locations, so their addresses can be assigned to pointers and invoked later. This enables callbacks, polymorphism, and dynamic function dispatch.

## Key Points
- Function pointers store the address of executable code, not data
- Syntax: `return_type (*ptr_name)(param_types)`
- Can assign existing functions: `ptr = &function` or `ptr = function`
- Invocation: `(*ptr)(args)` or `ptr(args)` (both valid)
- Used for callbacks, event handlers, and strategy pattern
- Arrays of function pointers enable jump tables

## Related Concepts
- [[pointers]]
- callbacks
- [[structures]]

## Examples
```c
// Basic function pointer declaration and usage
int add(int a, int b) {
    return a + b;
}

int main(void) {
    int (*ptr)(int, int) = &add;
    int result = (*ptr)(3, 4);  // result = 7
    result = ptr(3, 4);         // equivalent syntax
    return 0;
}

// Callback example
void transform(int *arr, int size, int (*func)(int)) {
    for (int i = 0; i < size; i++) {
        arr[i] = func(arr[i]);
    }
}

int square(int x) { return x * x; }

int main(void) {
    int nums[] = {1, 2, 3};
    transform(nums, 3, &square);
    return 0;
}
```

## Common Mistakes
- ❌ Forgetting parentheses around pointer name: `int *ptr(int, int)` declares a function returning `int*`, not a function pointer
- ❌ Not matching function signature exactly (parameter types and return type)
- ❌ Using `&` when not needed (both `&func` and `func` work, but one is clearer)
