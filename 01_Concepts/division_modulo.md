---
tags: [Concepts]
---


# Division and Modulo Operators

## What It Is
The division (`/`) and modulo (`%`) operators are integer operations that work together: division gives the quotient, modulo gives the remainder. Their relationship is defined by: `a == (a/b)*b + a%b`. Both operate on integers and produce integer results.

## Key Points
- Division `/` returns quotient (truncates toward zero in C99+)
- Modulo `%` returns remainder (sign matches sign of dividend in C99+)
- Both require non-zero right operand (division by zero is undefined)
- Truncation toward zero means `-7 / 2 == -3` (not -4)
- Modulo follows: `-7 % 2 == -1` (same sign as dividend)
- Essential for digit extraction, cyclic patterns, and separating components

## Related Concepts
- [[modulo_division]]
- [[digit_extraction]]
- math_operations

## Examples
```c
// Separate quotient and remainder
int divide_and_remainder(int a, int b, int *remainder) {
    *remainder = a % b;
    return a / b;
}

// Check if number is even or odd
int is_even(int n) {
    return n % 2 == 0;
}

// Convert minutes to hours and minutes
void minutes_to_hours_minutes(int total_min, int *hours, int *mins) {
    *hours = total_min / 60;
    *mins = total_min % 60;
}

// Check divisibility (multiple of any number)
int is_multiple(int n, int divisor) {
    return n % divisor == 0;
}

// Integer division behavior with negatives (C99+)
void division_examples(void) {
    // In C99+, truncation is toward zero:
    int a = -7 / 2;   // a = -3 (not -4)
    int b = -7 % 2;   // b = -1 (same sign as dividend)
    
    // In C89, truncation was implementation-defined
    // Always check your compiler's behavior for negative numbers
}
```

## Common Mistakes
- ❌ Division by zero (crashes/Undefined Behavior)
- ❌ Assuming integer division rounds instead of truncates
- ❌ Using modulo with negative numbers without understanding C99+ rules
- ❌ Confusing quotient and remainder when both are needed
