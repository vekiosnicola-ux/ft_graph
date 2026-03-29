---
tags: [Level_2, exam]
Level: 2
Topic: Algorithms
Exercise: is_power_of_2
---


# is_power_of_2

## What It Does
Returns 1 if `n` is a power of 2, otherwise returns 0.

## The Insight
Bitwise trick: powers of 2 have exactly one bit set in binary. `n & (n-1)` clears that bit. If result is 0, it was a power of 2.

## Step-by-Step Algorithm
`return (n > 0 && !(n & (n - 1)));`

## Code
```c
int is_power_of_2(unsigned int n)              // Function: takes unsigned int, returns int (1 or 0)
{
    return (n > 0 && !(n & (n - 1)));          // Return 1 if n>0 AND n&(n-1) equals 0
}
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int is_power_of_2(unsigned int n)` | Define function: takes unsigned int, returns int |
| `{` | Start of function body |
| `return (n > 0 && !(n & (n - 1)));` | Return 1 if n>0 AND (n AND n-1) equals 0 |
| `}` | End of function |

## Why `n & (n-1)` Works
For a power of 2 (e.g., 8 = 0b1000):
- n-1 = 7 = 0b0111
- n & (n-1) = 0b1000 & 0b0111 = 0

For non-powers (e.g., 6 = 0b0110):
- n-1 = 5 = 0b0101
- n & (n-1) = 0b0110 & 0b0101 = 0b0100 ≠ 0

## Common Traps
- ❌ Forgetting `n > 0` check (0 would incorrectly return 1)
- ❌ Forgetting parentheses around `n & (n-1)` (operator precedence)
- ❌ Not using unsigned int (negative numbers have complex representation)

## Related Exercises
- [[print_bits]] - Bit understanding
- gcd - Related mathematical algorithm

## Wiki Links
03_Exams/Level_2_INDEX|Level 2 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 58 lines)
