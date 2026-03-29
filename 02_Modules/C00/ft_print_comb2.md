---
tags: [C00, flashcard]
---


# ft_print_comb2

## What it does
Prints all unique pairs of two-digit numbers (00 to 99) in ascending order, separated by space and comma-space, with no trailing comma.

## The Insight
Two nested loops where `b = a + 1`. Each number is printed as two digits using `/` for tens and `%` for ones.

## Step-by-step Algorithm
1. Loop `a` from 0 to 98
2. Set `b = a + 1`, loop `b` from `a+1` to 99
3. Print `a` as two digits: `(a / 10) + '0'` and `(a % 10) + '0'`
4. Write a space
5. Print `b` similarly
6. If not last pair, write `", "`

## The Code (with pedagogical comments)
```c
 <unistd.h>  // Include library for system calls (write, read, close)

void ft_putchar(char c)  // Helper function: prints one character
{
    write(1, &c, 1);  // Write 1 byte from address of c to stdout
}

void ft_print_comb2(void)  // Function: returns nothing, takes nothing
{
    int a;  // First number (00-98)
    int b;  // Second number (a+1 to 99)

    a = 0;  // Start first number at 0
    while (a <= 98)  // First number goes up to 98 (need room for b)
    {
        b = a + 1;  // Second number starts one after first
        while (b <= 99)  // Second number goes up to 99
        {
            ft_putchar((a / 10) + '0');  // Extract tens digit of a and print
            ft_putchar((a % 10) + '0');  // Extract ones digit of a and print
            write(1, " ", 1);  // Write a space separator
            ft_putchar((b / 10) + '0');  // Extract tens digit of b and print
            ft_putchar((b % 10) + '0');  // Extract ones digit of b and print
            if (!(a == 98 && b == 99))  // If not the last pair (98, 99)
                write(1, ", ", 2);  // Write comma and space separator
            b++;  // Move to next second number
        }
        a++;  // Move to next first number
    }
}
```

## Line-by-Line Translation
1. `#include <unistd.h>` - Include the library for system calls
2. `void ft_putchar(char c)` - Define a helper function that prints one character
3. `write(1, &c, 1)` - Write 1 byte from the address of c to stdout
4. `void ft_print_comb2(void)` - Define the main function that returns nothing and takes nothing
5. `int a, b` - Create two integer variables for the two numbers
6. `a = 0` - Start the first number at 0
7. `while (a <= 98)` - Loop while first number is at most 98
8. `b = a + 1` - Set second number to one more than first
9. `while (b <= 99)` - Loop while second number is at most 99
10. `ft_putchar((a / 10) + '0')` - Extract and print the tens digit of a
11. `ft_putchar((a % 10) + '0')` - Extract and print the ones digit of a
12. `write(1, " ", 1)` - Write a space between the two numbers
13. `ft_putchar((b / 10) + '0')` - Extract and print the tens digit of b
14. `ft_putchar((b % 10) + '0')` - Extract and print the ones digit of b
15. `if (!(a == 98 && b == 99))` - Check if this is NOT the last combination
16. `write(1, ", ", 2)` - Write comma and space separator
17. `b++` - Move to the next second number
18. `a++` - Move to the next first number

## Common Traps
- ❌ Using `printf` instead of `write`
- ❌ Printing trailing comma after last pair
- ❌ Forgetting to convert digits to characters (`+'0'`)
- ❌ Using `char` for loop variables (works but `int` is clearer)

## Related Concepts
- 01_Concepts/digit_extraction|Digit Extraction
- 01_Concepts/modulo_division|Modulo Division

## Related Exercises
- [[ft_print_comb]]
- [[ft_print_combn]]

## Propedeuticity
**Prerequisites:** [[ft_print_comb]]
**Unlocks:** [[ft_print_combn]]

How do you print a two-digit number?
::
```c
ft_putchar((n / 10) + '0');  // Tens digit
ft_putchar((n % 10) + '0');  // Ones digit
```
