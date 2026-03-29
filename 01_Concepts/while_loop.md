---
tags: [Concepts]
---


# While Loop

## What It Is
The while loop repeatedly executes a statement (or block) as long as its condition evaluates to true (non-zero). It's the fundamental looping construct in C, used when the number of iterations is not known in advance. The condition is checked before each iteration.

## Key Points
- `while (condition) statement` - check condition first, then execute
- `do statement while (condition)` - execute first, then check (runs at least once)
- Condition is evaluated each iteration: 0 = stop, non-zero = continue
- Must ensure loop makes progress toward termination (update condition variables)
- The "skeleton pattern": `int i = 0; while (condition) { ... i++; }`

## Related Concepts
- loop_invariants
- infinite_loops
- skeleton_pattern

## Examples
```c
// Print 0 to 9 (skeleton pattern)
int i = 0;
while (i < 10) {
    write(1, &"0123456789"[i], 1);
    i++;
}

// Iterate through string
void print_string(const char *str) {
    int i = 0;
    while (str[i] != '\0') {
        write(1, &str[i], 1);
        i++;
    }
}

// Find first matching character
char *find_char(const char *str, char target) {
    int i = 0;
    while (str[i] != '\0') {
        if (str[i] == target)
            return (char *)&str[i];  // found
        i++;
    }
    return NULL;  // not found
}

// Do-while (always runs at least once)
int get_positive(void) {
    int n;
    do {
        // read input into n
    } while (n <= 0);
    return n;
}

// While true with break (alternative structure)
void process_items(int *arr, int size) {
    int i = 0;
    while (1) {
        if (i >= size)
            break;
        // process arr[i]
        i++;
    }
}

// Nested while loops
void multiplication_table(void) {
    int row = 1;
    while (row <= 9) {
        int col = 1;
        while (col <= 9) {
            // print product
            col++;
        }
        row++;
    }
}
```

## Common Mistakes
- ❌ Forgetting to increment loop variable (infinite loop)
- ❌ Off-by-one errors in condition (using `<=` vs `<`)
- ❌ Forgetting braces for multi-statement loops (only first statement executes in loop)
- ❌ Not initializing loop variable before first check
- ❌ Accidental trailing semicolon: `while (cond);` creates empty loop body
