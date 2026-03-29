---
tags: [Level_4, exam]
  - math
  - factors
  - white
---


# fprime

## What it does
Prints prime factors of a number separated by '*'. e.g. 12 -> 2*2*3

## The Insight
Start with divisor=1. Loop: if n%div==0, print div, divide n by div, reset div=1. This finds smallest prime each time.

## Step-by-step Algorithm
1. div=1
2. Loop while n>div
3. if n%div==0: print div, if n==div break, print '*', n/=div, div=1
4. Special case n=1 -> print 1

## The Code
```c
// fprime: Prints prime factorization of a number
// Example: 12 -> "2*2*3", 5 -> "5", 1 -> "1"

void fprime(int nbr)
{
    int div = 1;                         // Start divisor at 1
    if (nbr < 0)                        // Handle negative input
        return;
    if (nbr == 1)                       // Special case: 1 prints as "1"
    {
        write(1, "1", 1);               // Write the character '1'
        return;                         // Exit function
    }
    while (nbr > div++)                  // Loop: while nbr > divisor (post-increment div)
    {
        if (nbr % div == 0)              // If divisor divides evenly into nbr
        {
            putnbr(div);                 // Print the divisor
            if (nbr == div)              // If nbr equals divisor, we're done
                break;                   // Exit the loop
            write(1, "*", 1);            // Print '*' separator
            nbr /= div;                  // Divide nbr by divisor to continue
            div = 1;                     // RESET divisor to 1 (critical for prime factors)
        }
    }
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 21 | `void fprime(int nbr)` | Function takes integer parameter |
| 22 | `int div = 1;` | Initialize divisor to 1 (smallest possible factor) |
| 23-24 | `if (nbr < 0) return;` | Reject negative numbers (no prime factors for negatives) |
| 25-30 | `if (nbr == 1) {...}` | Special case: 1 should print as "1" |
| 31 | `while (nbr > div++)` | Main loop: while nbr > divisor, increment div after comparison |
| 33 | `if (nbr % div == 0)` | Check if current divisor divides nbr evenly (is a factor) |
| 35 | `putnbr(div);` | Print the divisor (factor) |
| 36-37 | `if (nbr == div) break;` | If nbr equals div, we've found all factors - exit |
| 38 | `write(1, "*", 1);` | Print '*' as separator between factors |
| 39 | `nbr /= div;` | Divide nbr by the factor we just found |
| 40 | `div = 1;` | RESET div to 1 to start finding next (smaller) factor |

## Common Traps
- ❌ Infinite loop (must reset div=1 after finding factor - without this, stuck at same divisor)
- ❌ Not handling n=1 (special case needed, loop wouldn't run for n=1)
- ❌ Wrong divisor start (must start at 1, not 2, to catch all prime factors)

## Related
- [[sort_int_tab]] - sorting
- [[ft_itoa]] - number to string
- EXAMS INDEX|Exam INDEX
