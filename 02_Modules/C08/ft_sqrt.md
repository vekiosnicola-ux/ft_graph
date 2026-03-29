---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# ft_sqrt

---
tags: [C08, magenta]
---

## Navigation
← [[ft_sort_arr_int|ft_sort_arr_int]] | [[ft_find_next_prime|Next: ft_find_next_prime →]]

## What it does
Returns the integer square root of a given number. Returns 0 if the number is not a perfect square.

## The Insight
Try all possible candidates from 1 to `n / 2`. The square root of n cannot exceed n/2 for n > 1.

## Step-by-step Algorithm
1. Handle edge cases: n < 0 returns 0.
2. If n == 0 or n == 1, return n.
3. Initialize `i = 1`.
4. While `i * i <= n`:
   a. If `i * i == n`, return `i`.
   b. Increment `i`.
5. Return 0 (not a perfect square).

## The Code
```c
 <stdlib.h>  // Included for consistency (no malloc used here)

int ft_sqrt(int nb)  // Computes integer square root of nb
{
    int i;  // Candidate square root value being tested

    if (nb < 0)  // Negative numbers have no real square root
        return (0);  // Return 0 to indicate "not a perfect square"
    if (nb == 0 || nb == 1)  // Base cases: sqrt(0) = 0, sqrt(1) = 1
        return (nb);  // Return the number itself (0 or 1)
    i = 1;  // Start testing candidates from 1
    while (i <= nb / 2)  // No candidate can exceed nb divided by 2
    {
        if (i * i == nb)  // If current candidate squared equals target
            return (i);  // Found it! Return the square root
        i++;  // Try the next candidate
    }
    return (0);  // No integer square root found - not a perfect square
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 23 | `#include <stdlib.h>` | Include standard library header |
| 25 | `int ft_sqrt(int nb)` | Returns integer square root; 0 means "not perfect square" |
| 27 | `int i;` | Candidate value we're testing as the square root |
| 29 | `if (nb < 0)` | Negative numbers don't have real integer square roots |
| 30 | `return (0);` | Signal that sqrt doesn't exist for negative input |
| 31 | `if (nb == 0 \|\| nb == 1)` | Special cases where result is the input itself |
| 32 | `return (nb);` | Return 0 or 1 directly |
| 33 | `i = 1;` | Begin testing potential square roots starting at 1 |
| 34 | `while (i <= nb / 2)` | Optimization: sqrt(n) can never be more than n/2 for n > 1 |
| 36 | `if (i * i == nb)` | Test: does this candidate squared equal our target? |
| 37 | `return (i);` | Success! We found the integer square root |
| 38 | `i++;` | Not this candidate - try the next integer |
| 40 | `return (0);` | Exhausted all possibilities - not a perfect square |

## Common Traps
- ❌ Not handling negative numbers.
- ❌ Going up to `nb` instead of `nb / 2`.
- ❌ Integer overflow when multiplying `i * i`.

## Related Concepts
- 01_Concepts/math|Mathematical Operations

## Related Exercises
- [[ft_find_next_prime]]

How do you find integer square root?
::
Try candidates from 1 to n/2, return when i*i == n.
