---
tags: [Level_3, exam]
  - euclidean-algorithm
  - white
Level: 3
Topic: Algorithms
Exercise: lcm
---


# lcm

## What It Does
Returns the Least Common Multiple of two positive integers.

## The Insight
`LCM(a,b) = (a * b) / GCD(a,b)`. Use Euclidean algorithm for GCD (recursive), then divide to get LCM.

## Step-by-Step Algorithm
1. GCD via recursion: `gcd(a,b) = b==0 ? a : gcd(b, a%b)`
2. `lcm = (a / gcd) * b` (divide first to avoid overflow)
3. Return lcm

## Code
```c
unsigned int gcd(unsigned int a, unsigned int b)   // Helper: computes GCD using Euclidean algorithm
{
    return b == 0 ? a : gcd(b, a % b);             // If b is 0, a is GCD; else recurse with b and a%b
}

unsigned int lcm(unsigned int a, unsigned int b)   // Function: computes LCM of a and b
{
    // Return 0 if either is 0, otherwise (a / GCD) * b to avoid overflow
    return a == 0 || b == 0 ? 0 : (a / gcd(a, b)) * b;
}
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `unsigned int gcd(unsigned int a, unsigned int b)` | Define GCD helper function |
| `return b == 0 ? a : gcd(b, a % b);` | Return a if b is 0, else recurse with b and remainder |
| `unsigned int lcm(unsigned int a, unsigned int b)` | Define LCM function |
| `return a == 0 \|\| b == 0 ? 0 : (a / gcd(a, b)) * b;` | Return 0 if either is 0, else (a/GCD)*b |

## Why Divide First?
`(a / gcd) * b` avoids overflow that `(a * b) / gcd` could cause when a and b are large.

## Common Traps
- ❌ Division by zero when a or b is 0 (handle this case explicitly)
- ❌ Integer overflow in `a * b` before dividing (must divide by GCD first)
- ❌ Not using unsigned int (prevents issues with negative numbers)
- ❌ Forgetting the GCD helper function

## Related Exercises
- [[pgcd]] - GCD calculation
- [[is_power_of_2]] - Related bit trick

## Wiki Links
03_Exams/Level_3_INDEX|Level 3 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 44 lines)
