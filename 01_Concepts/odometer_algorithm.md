---
tags: [Concepts]
---


# Odometer Algorithm

## What It Is
The odometer algorithm generates combinations or sequences by treating digits like an odometer counter. Each "wheel" (position) has a maximum value, and when one wheel overflows, it resets to its starting value and the next wheel increments. Used in `ft_print_combn` and similar problems.

## Key Points
- Mimics how a car odometer increments: rightmost digit rolls over, next digit increments
- Each position has its own maximum (e.g., for combinations of n digits, last position max is '9', second-to-last is '8', etc.)
- Generates sequences in lexicographic order automatically
- Reset all wheels to the right when incrementing occurs
- Essential for generating combinations without repetition

## Related Concepts
- [[lexicographic_order]]
- [[sorting_algorithms]]
- [[ft_print_combn]]

## Examples
```c
// Odometer increment for combination printing
// Given digits[] = {0, 1, 4, ...}, increment the rightmost possible wheel
void odometer_increment(char *digits, int n) {
    int i = n - 1;
    
    // Find rightmost digit that can be incremented
    while (i >= 0 && digits[i] == '9' - (n - 1 - i))
        i--;
    
    if (i < 0)  // All digits at max, done
        return;
    
    digits[i]++;  // Increment this position
    
    // Reset all positions to the right to be consecutive after the incremented one
    for (int j = i + 1; j < n; j++) {
        digits[j] = digits[j - 1] + 1;
    }
}

// Example: for n=4, sequence is:
// 0123, 0124, 0125, ..., 0129
// 0134, 0135, ..., 0139
// ...
// 6789
```

## Common Mistakes
- ❌ Forgetting to calculate each position's maximum (depends on index from right)
- ❌ Not resetting wheels to the right after incrementing
- ❌ Not detecting when all wheels are at maximum (end condition)
