---
tags: [Concepts]
---


# Conditional Statements

## What It Is
Conditional statements control program flow based on boolean expressions. They enable branching logic where different code executes depending on whether conditions are true or false. Essential for decision-making in any program.

## Key Points
- `if (condition) statement` - executes if condition is true (non-zero)
- `else statement` - executes if previous if was false
- `else if (condition) statement` - chains multiple conditions
- Ternary operator: `cond ? expr1 : expr2`
- Condition should evaluate to int: 0 = false, non-zero = true
- `switch` provides multi-way branching for discrete values

## Related Concepts
- boolean_logic
- ternary_operator
- switch_statement

## Examples
```c
// Basic if-else
int max(int a, int b) {
    if (a > b)
        return a;
    else
        return b;
}

// Chain of conditions
const char *grade(int score) {
    if (score >= 90)
        return "A";
    else if (score >= 80)
        return "B";
    else if (score >= 70)
        return "C";
    else if (score >= 60)
        return "D";
    else
        return "F";
}

// Ternary operator
int abs_val(int n) {
    return n >= 0 ? n : -n;
}

int max三元(int a, int b) {
    return (a > b) ? a : b;
}

// Nested if with else binding
void example(int x, int y) {
    if (x > 0)
        if (y > 0)
            write(1, "both positive\n", 15);
    else
        write(1, "x not positive\n", 16);  // else binds to inner if!
}

// Correct way with braces
void example_fixed(int x, int y) {
    if (x > 0) {
        if (y > 0)
            write(1, "both positive\n", 15);
    } else {
        write(1, "x not positive\n", 16);
    }
}

// Switch statement
void digit_to_word(int d) {
    switch (d) {
        case 0: write(1, "zero", 4); break;
        case 1: write(1, "one", 3); break;
        case 2: write(1, "two", 3); break;
        default: write(1, "other", 5);
    }
}
```

## Common Mistakes
- ❌ Forgetting braces with nested if-else (else binds to nearest if, not intended)
- ❌ Using `=` instead of `==` in condition (assigns instead of compares)
- ❌ Forgetting break in switch (causes fall-through to next case)
- ❌ Using switch with non-constant or non-discrete values (use if-else instead)
- ❌ Confusing `else if` as new statement (it's else + if combined)
