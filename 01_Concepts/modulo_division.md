---
tags: [Concepts]
---


# Modulo Division

## What It Is
The modulo operator (`%`) returns the remainder after integer division. It's essential for cyclic patterns, wrapping values within a range, determining if numbers are divisible, and implementing circular behavior. Often used with division (`/`) to separate quotient and remainder.

## Key Points
- `a % b` returns remainder when a is divided by b (b must be non-zero)
- `a == a / b * b + a % b` (fundamental theorem of division)
- Used to detect multiples: `n % 3 == 0` means n is divisible by 3
- Wrapping/clamping: `value % max` keeps value in [0, max-1] range
- Negative numbers with modulo have implementation-defined sign in C89, defined in C99+

## Related Concepts
- [[division_modulo]]
- [[digit_extraction]]
- [[modulo_division]]

## Examples
```c
// Fizzbuzz: divisible by 3="fizz", 5="buzz", 15="fizzbuzz"
void fizzbuzz(void) {
    for (int i = 1; i <= 100; i++) {
        if (i % 15 == 0)
            write(1, "fizzbuzz", 8);
        else if (i % 3 == 0)
            write(1, "fizz", 4);
        else if (i % 5 == 0)
            write(1, "buzz", 4);
        else {
            char c = '0' + i;
            write(1, &c, 1);
        }
    }
}

// Cyclic array access (circular buffer pattern)
int circular_access(int *arr, int size, int index) {
    return arr[index % size];  // wraps around
}

// Determine if year is leap year
int is_leap_year(int year) {
    return (year % 4 == 0 && year % 100 != 0) || (year % 400 == 0);
}

// Sum of digits using modulo
int sum_of_digits(int n) {
    int sum = 0;
    while (n != 0) {
        sum += n % 10;
        n /= 10;
    }
    return sum;
}
```

## Common Mistakes
- ❌ Using modulo with negative numbers (behavior varies: C99+ ensures positive remainder with a % b same sign as a)
- ❌ Forgetting that modulo by zero is undefined (crashes)
- ❌ Confusing modulo with fraction (modulo is for integers only in C)
