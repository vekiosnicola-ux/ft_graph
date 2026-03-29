---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# ft_find_next_prime

---
tags: [C08, magenta]
---

## Navigation
← [[ft_sqrt|ft_sqrt]] | C08_INDEX|C08 INDEX →

## What it does
Finds the next prime number greater than or equal to the given number.

## The Insight
Check each number sequentially for primality. A number is prime if it's not divisible by any number from 2 to its square root.

## Step-by-step Algorithm
1. Handle edge cases (0, 1, 2).
2. Start at `n` and increment.
3. For each candidate `n`:
   a. Check divisibility from 2 to `sqrt(n)`.
   b. If no divisor found, return `n`.
   c. Else, increment `n` and repeat.

## The Code
```c
 <stdlib.h>  // Included for consistency

// Helper function: checks if a number is prime
int ft_is_prime(int nb)  // Returns 1 if prime, 0 if not prime
{
    int i;  // Divisor being tested (checks 2, 3, 4, ... up to sqrt(nb))

    if (nb < 2)  // Numbers less than 2 cannot be prime (0 and 1 are not prime)
        return (0);  // Return "not prime"
    i = 2;  // Start testing divisors from 2 (smallest prime)
    while (i * i <= nb)  // Only need to check up to sqrt(nb); if nb has a factor
    {                      // larger than sqrt, it must also have one smaller than sqrt
        if (nb % i == 0)  // If nb divides evenly by i (remainder is 0)
            return (0);  // Found a divisor - nb is not prime
        i++;  // Try the next potential divisor
    }
    return (1);  // No divisors found - nb is prime
}

// Main function: finds next prime >= nb
int ft_find_next_prime(int nb)  // Returns the smallest prime >= nb
{
    if (nb < 2)  // Special case: next prime after 0 or 1 is 2
        return (2);  // The first prime number
    while (!ft_is_prime(nb))  // Keep checking numbers until we find a prime
        nb++;  // Try the next number
    return (nb);  // Found! Return the prime number
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 24 | `int ft_is_prime(int nb)` | Helper function: determines if nb is prime |
| 26 | `int i;` | Divisor variable for testing primality |
| 28 | `if (nb < 2)` | 0 and 1 are not prime numbers |
| 29 | `return (0);` | Signal that nb fails the prime test |
| 30 | `i = 2;` | Smallest possible prime divisor to test |
| 31 | `while (i * i <= nb)` | Only test up to the square root (math optimization) |
| 33 | `if (nb % i == 0)` | If i divides nb evenly with no remainder |
| 34 | `return (0);` | Found a divisor - nb cannot be prime |
| 35 | `i++;` | Try the next potential divisor |
| 37 | `return (1);` | No divisors found - nb IS prime |
| 40 | `int ft_find_next_prime(int nb)` | Main function that finds next prime >= nb |
| 42 | `if (nb < 2)` | Edge case: primes start at 2 |
| 43 | `return (2);` | Return 2 as the first prime |
| 44 | `while (!ft_is_prime(nb))` | Keep looping while current number isn't prime |
| 45 | `nb++;` | Check the next integer |
| 46 | `return (nb);` | Prime found - return it |

## Common Traps
- ❌ Forgetting that 0 and 1 are not prime.
- ❌ Not checking up to `sqrt(n)`.
- ❌ Off-by-one errors in the loop condition.

## Related Concepts
- 01_Concepts/recursion|Recursion
- 01_Concepts/math|Mathematical Operations

## Related Exercises
- [[ft_sqrt]]

How do you check if a number is prime?
::
Check divisibility from 2 to sqrt(n). If no divisor found, it's prime.
