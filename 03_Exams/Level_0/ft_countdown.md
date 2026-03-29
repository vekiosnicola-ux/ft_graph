---
tags: []
date: 2026-03-29
status: complete
---
# ft_countdown

EXAMS INDEX|Exam INDEX | Level 0

---
tags: [Exams, Level_0, magenta]
---


## What it does
Prints a countdown from 99 to 0, each number followed by a newline.

## Insight
This teaches you how to loop with a counter and print numbers. The key insight is that you need to:
1. Start at 99
2. Loop while >= 0
3. Print each number
4. Decrement the counter
5. Each number gets its own line (so you need \n after each)

This also introduces the recursive ft_putnbr pattern for printing integers.

## Step-by-step Algorithm
1. Initialize counter i = 99
2. While i >= 0:
   - Print the number i (using ft_putnbr or equivalent)
   - Write a newline
   - Decrement i
3. When i < 0, exit

## Code
```c
 <unistd.h>       // Required for write() system call

void ft_putnbr(int nb)    // Recursive function to print an integer
{
    if (nb < 0)           // If number is negative
    {
        write(1, "-", 1);  // Write minus sign
        nb = -nb;           // Make number positive for processing
    }
    if (nb >= 10)         // If number has two or more digits
        ft_putnbr(nb / 10);  // Recursively print all digits except last
    write(1, &"0123456789"[nb % 10], 1);  // Write last digit using lookup table
}

void ft_countdown(void)   // Main countdown function
{
    int i = 99;           // Start countdown from 99
    
    while (i >= 0)        // Loop while i is greater than or equal to 0
    {
        ft_putnbr(i);     // Print the current number
        write(1, "\n", 1);  // Print newline after each number
        i--;              // Decrement counter (MOVE TOWARD END CONDITION!)
    }
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|-------------|
| 1 | `#include <unistd.h>` | Include header for `write()` system call |
| 3 | `void ft_putnbr(int nb)` | Define recursive function to print integer |
| 4 | `{` | Start of ft_putnbr body |
| 5 | `if (nb < 0)` | Check if number is negative |
| 6 | `{` | Start of negative handling block |
| 7 | `write(1, "-", 1);` | Write minus sign to stdout |
| 8 | `nb = -nb;` | Convert negative to positive |
| 9 | `}` | End of negative handling block |
| 10 | `if (nb >= 10)` | Check if number has multiple digits |
| 11 | `ft_putnbr(nb / 10);` | Recursively call with all digits except last |
| 12 | `write(1, &"0123456789"[nb % 10], 1);` | Write last digit using array lookup |
| 13 | `}` | End of ft_putnbr function |
| 15 | `void ft_countdown(void)` | Define countdown function (no parameters) |
| 16 | `{` | Start of ft_countdown body |
| 17 | `int i = 99;` | Initialize counter to 99 |
| 18 | `while (i >= 0)` | Loop while counter is >= 0 |
| 19 | `{` | Start of while body |
| 20 | `ft_putnbr(i);` | Print current countdown number |
| 21 | `write(1, "\n", 1);` | Print newline after number |
| 22 | `i--;` | Decrement counter (CRITICAL: prevents infinite loop) |
| 23 | `}` | End of while body |
| 24 | `}` | End of ft_countdown |

## Common Traps
- ❌ Starting at 100 instead of 99
- ❌ Using while (i > 0) instead of while (i >= 0) (misses 0)
- ❌ Forgetting to decrement i (infinite loop)
- ❌ Not writing newline after each number
- ❌ Using printf instead of write/ft_putnbr
- ❌ Not handling negative numbers in ft_putnbr (though not needed here since we start positive)

## Propedeuticity
- [[ft_print_numbers]] - Simple counting loop
- [[hello]] - Basic write output

## Related Exercises
- [[ft_print_numbers]] - Forward counting from 0 to 9

(End of file - 92 lines)
