---
tags: []
date: 2026-03-29
status: complete
---
# fizzbuzz

EXAMS INDEX|Exam INDEX | Level 1

---
tags: [Exams, Level_1, magenta]
---

## What it does
Prints numbers from 1 to 100, but:
- For multiples of 3, prints "fizz" instead of the number
- For multiples of 5, prints "buzz" instead of the number
- For multiples of both 3 and 5 (i.e., multiples of 15), prints "fizzbuzz"
- Each output is followed by a newline

## Insight
This teaches you how to handle multiple conditions and modular arithmetic. The key insight is:
1. Check for the most specific condition first (divisible by both 3 and 5 → divisible by 15)
2. Then check for the individual conditions (divisible by 3, divisible by 5)
3. Otherwise, print the number

This is the classic "hierarchy of conditions" pattern.

## Step-by-step Algorithm
1. Initialize counter i = 1
2. While i <= 100:
   - If i % 15 == 0, write "fizzbuzz"
   - Else if i % 3 == 0, write "fizz"
   - Else if i % 5 == 0, write "buzz"
   - Else, write the number i (using ft_putnbr)
   - Write a newline after each output
   - Increment i
3. When i > 100, exit

## Code
```c
 <unistd.h>       // Required for write() system call

void ft_putnbr(int nb)    // Recursive function to print an integer
{
    if (nb < 0)           // If number is negative
    {
        write(1, "-", 1);  // Write minus sign
        nb = -nb;           // Make number positive
    }
    if (nb >= 10)         // If number has multiple digits
        ft_putnbr(nb / 10);  // Recursively print all digits except last
    write(1, &"0123456789"[nb % 10], 1);  // Write last digit using lookup table
}

void fizzbuzz(int len)    // Main fizzbuzz function, len = 100
{
    int i = 1;           // Start counting from 1 (not 0!)
    
    while (i <= len)     // Loop from 1 to len (inclusive)
    {
        if (i % 15 == 0)      // If divisible by BOTH 3 and 5 (multiple of 15)
            write(1, "fizzbuzz", 8);  // Write "fizzbuzz" (8 bytes)
        else if (i % 3 == 0)  // Else if divisible by 3 only
            write(1, "fizz", 4);     // Write "fizz" (4 bytes)
        else if (i % 5 == 0)  // Else if divisible by 5 only
            write(1, "buzz", 4);     // Write "buzz" (4 bytes)
        else                  // Otherwise
            ft_putnbr(i);     // Print the number itself
        write(1, "\n", 1);  // Newline after each output
        i++;                // Increment counter
    }
}

int main(void)            // Main takes no arguments
{
    fizzbuzz(100);        // Call fizzbuzz with 100
    return (0);           // Exit with success
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|-------------|
| 1 | `#include <unistd.h>` | Include header for `write()` system call |
| 3 | `void ft_putnbr(int nb)` | Define recursive function to print integer |
| 4 | `{` | Start of ft_putnbr body |
| 5 | `if (nb < 0)` | Check if number is negative |
| 6 | `{` | Start of negative block |
| 7 | `write(1, "-", 1);` | Write minus sign |
| 8 | `nb = -nb;` | Convert to positive |
| 9 | `}` | End of negative block |
| 10 | `if (nb >= 10)` | Check if multiple digits |
| 11 | `ft_putnbr(nb / 10);` | Recurse with n/10 (all but last digit) |
| 12 | `write(1, &"0123456789"[nb % 10], 1);` | Write last digit |
| 13 | `}` | End of ft_putnbr |
| 15 | `void fizzbuzz(int len)` | Define fizzbuzz function |
| 16 | `{` | Start of fizzbuzz body |
| 17 | `int i = 1;` | Initialize counter to 1 |
| 18 | `while (i <= len)` | Loop while i <= len |
| 19 | `{` | Start of while body |
| 20 | `if (i % 15 == 0)` | Check if divisible by both 3 AND 5 |
| 21 | `write(1, "fizzbuzz", 8);` | Write "fizzbuzz" (8 bytes) |
| 22 | `else if (i % 3 == 0)` | Check if divisible by 3 only |
| 23 | `write(1, "fizz", 4);` | Write "fizz" |
| 24 | `else if (i % 5 == 0)` | Check if divisible by 5 only |
| 25 | `write(1, "buzz", 4);` | Write "buzz" |
| 26 | `else` | None of the above |
| 27 | `ft_putnbr(i);` | Print the number |
| 28 | `write(1, "\n", 1);` | Print newline |
| 29 | `i++;` | Increment counter |
| 30 | `}` | End of while body |
| 31 | `}` | End of fizzbuzz |
| 32 | `int main(void)` | Main with no arguments |
| 33 | `{` | Start of main body |
| 34 | `fizzbuzz(100);` | Call fizzbuzz with upper limit 100 |
| 35 | `return (0);` | Exit with success |
| 36 | `}` | End of main |

## Common Traps
- ❌ Checking for 3 and 5 before 15 (would never reach "fizzbuzz" case)
- ❌ Using wrong string lengths: "fizz"=4, "buzz"=4, "fizzbuzz"=8
- ❌ Forgetting the newline after each output
- ❌ Starting at 0 instead of 1
- ❌ Using while (i < 100) instead of while (i <= 100) (misses 100)
- ❌ Not incrementing i (infinite loop)
- ❌ Using printf instead of write/ft_putnbr

## Propedeuticity
- [[ft_print_numbers]] - Basic counting loop
- [[ft_countdown]] - Number printing with loops

## Related Exercises
- [[ft_print_numbers]] - Simple number iteration
- [[ft_countdown]] - Counting down numbers

(End of file - 124 lines)
