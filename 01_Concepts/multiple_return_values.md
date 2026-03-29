---
tags: [Concepts]
---


# Multiple Return Values

## What It Is
C functions can return only one value, but multiple values can be obtained through output parameters (pointers). The function modifies variables in the caller by receiving their addresses. This pattern is essential for functions like `div_mod`, `swap`, or any function that needs to "return" more than one piece of information.

## Key Points
- Use pointers to pass addresses of variables to be modified
- Function signature indicates which parameters are output (pointers) vs input (values)
- Caller must pass addresses (`&var`), not values
- Common pattern: `void function(inputs, *output1, *output2)`
- Enables functions to "return" multiple values simultaneously

## Related Concepts
- [[pointers]]
- [[ft_div_mod]]
- [[ft_swap]]
- [[pointers_to_pointers]]

## Examples
```c
// Return quotient and remainder via pointers
void div_mod(int a, int b, int *quotient, int *remainder) {
    if (b != 0) {
        *quotient = a / b;
        *remainder = a % b;
    }
}

int main(void) {
    int q, r;
    div_mod(17, 5, &q, &r);  // q=3, r=2
    return 0;
}

// Swap two values (modifies original variables)
void swap(int *a, int *b) {
    int temp = *a;
    *a = *b;
    *b = temp;
}

// Return coordinates from a string parsing function
int parse_coordinate(const char *str, int *x, int *y) {
    // Parse "x,y" format
    int parsed = sscanf(str, "%d,%d", x, y);
    return parsed == 2;
}

// Boolean success + value via pointer
int find_min(int *arr, int size, int *min_val) {
    if (size <= 0) return 0;  // error
    *min_val = arr[0];
    for (int i = 1; i < size; i++) {
        if (arr[i] < *min_val)
            *min_val = arr[i];
    }
    return 1;  // success
}
```

## Common Mistakes
- ❌ Forgetting to pass addresses (`&var`) instead of values (would modify local copies)
- ❌ Not initializing output variables before the call (they get written, not read)
- ❌ Passing NULL for pointer parameters when function expects valid address
- ❌ Not checking for error conditions (like size == 0)
