---
tags: [C00, flashcard]
---


# ft_putnbr

## Navigation
← [[ft_print_comb2|ft_print_comb2]] | [[ft_print_combn|Next: ft_print_combn →]]

## What it does
Prints any integer (including negative numbers and INT_MIN) to stdout using recursion.

## The Insight
Recursion processes digits from most significant to least: recurse first, print last. Converting to `long long` handles INT_MIN safely.

## Step-by-step Algorithm
1. Convert `int nb` to `long long n` (handles INT_MIN)
2. If negative, print '-' and negate
3. If `n >= 10`, recurse with `n / 10`
4. Print last digit: `(n % 10) + '0'`

## The Code (with pedagogical comments)
```c
 <unistd.h>  // Include library for system calls
 <limits.h>  // Include library for INT_MIN, INT_MAX

void ft_putchar(char c)  // Helper function to print one character
{
    write(1, &c, 1);  // Write 1 byte from address of c to stdout
}

void ft_putnbr(int nb)  // Function: returns nothing, takes an integer
{
    long long n;  // Use long long to handle INT_MIN safely

    if (nb < 0)  // If number is negative
    {
        ft_putchar('-');  // Print minus sign
        n = -(long long)nb;  // Convert to positive long long (safe negation)
    }
    else  // If number is positive or zero
        n = (long long)nb;  // Convert to long long
    if (n >= 10)  // If number has more than one digit
        ft_putnbr(n / 10);  // Recursively print higher digits first
    ft_putchar((n % 10) + '0');  // Print last digit (convert to ASCII)
}
```

## Line-by-Line Translation
1. `#include <unistd.h>` - Include the library for system calls
2. `#include <limits.h>` - Include the library for integer limits (INT_MIN, INT_MAX)
3. `void ft_putchar(char c)` - Define a helper function that prints one character
4. `write(1, &c, 1)` - Write 1 byte from the address of c to stdout
5. `void ft_putnbr(int nb)` - Define the main function that takes an integer
6. `long long n` - Create a long long variable to handle INT_MIN safely
7. `if (nb < 0)` - Check if the number is negative
8. `ft_putchar('-')` - Print a minus sign
9. `n = -(long long)nb` - Safely negate the number by converting to long long first
10. `else` - If the number is positive or zero
11. `n = (long long)nb` - Convert the number to long long
12. `if (n >= 10)` - Check if the number has more than one digit
13. `ft_putnbr(n / 10)` - Recursively print the higher digits first
14. `ft_putchar((n % 10) + '0')` - Print the last digit by converting to ASCII

## Common Traps
- ❌ Using `printf` instead of `write`
- ❌ Forgetting to handle INT_MIN (negating INT_MIN overflows)
- ❌ Printing digits in wrong order (must recurse before printing)
- ❌ Not converting to `long long`

## Related Concepts
- 01_Concepts/recursion|Recursion
- 07_Manual/c_stdlib.h|stdlib.h

## Related Exercises
- [[ft_print_numbers]]
- [[ft_print_combn]]

## Propedeuticity
**Prerequisites:** [[ft_print_numbers]], [[ft_is_negative]]
**Unlocks:** [[ft_print_combn]], exam recursion questions

How do you print an integer recursively?
::
```c
if (n >= 10)
    ft_putnbr(n / 10);  // Print higher digits first
ft_putchar((n % 10) + '0');  // Print last digit
```
