---
tags: [Concepts]
---


# Math Operations in C

## What It Is
C provides arithmetic operators for integer and floating-point mathematics. Integer operations have specific behaviors around overflow, division truncation, and edge cases like INT_MIN. Understanding these behaviors is critical for writing correct numeric code.

## Key Points
- Integer overflow is undefined behavior (can wrap, saturate, or crash depending on compiler/flags)
- Division truncates toward zero (C99+): `-7/2 == -3`, not `-4`
- Use `long long` or careful ordering when negating INT_MIN (can't negate -2147483648 in int)
- Modulo follows sign of dividend (C99+): `-7%2 == -1`
- Floating-point math has precision limits; use double for better precision
- Bit shifts on signed types have implementation-defined behavior

## Related Concepts
- [[division_modulo]]
- int_min_edge_case
- [[ft_putnbr]]
- [[ft_atoi]]

## Examples
```c
 <limits.h>
 <math.h>

// Safe negation of INT_MIN requires cast to long long
long long safe_negate(int n) {
    return -(long long)n;
}

// Detect potential overflow before addition
int safe_add(int a, int b) {
    if (a > 0 && b > INT_MAX - a)  // would overflow
        return INT_MAX;
    if (a < 0 && b < INT_MIN - a)  // would underflow
        return INT_MIN;
    return a + b;
}

// Absolute value (handling INT_MIN specially)
int my_abs(int n) {
    if (n == INT_MIN)  // can't negate safely
        return INT_MAX;  // or handle as special case
    return n >= 0 ? n : -n;
}

// Integer division truncation behavior
void division_demo(void) {
    int a = 7 / 2;    // a = 3 (truncates)
    int b = -7 / 2;   // b = -3 (truncates toward zero)
    int c = 7 % 2;    // c = 1
    int d = -7 % 2;   // d = -1 (sign of dividend)
}

// Power without pow() for integers
long long int_pow(int base, int exp) {
    long long result = 1;
    while (exp > 0) {
        if (exp % 2 == 1)
            result *= base;
        base *= base;
        exp /= 2;
    }
    return result;
}

// Check if number is power of 2
int is_power_of_2(int n) {
    return n > 0 && (n & (n - 1)) == 0;
}
```

## Common Mistakes
- ❌ Assuming integer overflow wraps around (undefined behavior)
- ❌ Negating INT_MIN without cast (overflows in int)
- ❌ Using `a / b` and expecting mathematical division result
- ❌ Forgetting that `%` is remainder, not modulo (sign matters)
- ❌ Comparing floating-point with `==` (use epsilon comparison)
