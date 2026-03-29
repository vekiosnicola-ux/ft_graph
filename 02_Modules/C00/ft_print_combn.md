---
tags: [C00, flashcard]
---


# ft_print_combn

## What it does
Prints all unique combinations of `n` digits (0-9) in ascending order, separated by comma-space, with no trailing comma. `n` is 1-9.

## The Insight
Odometer approach: array of `n` digits starts at `0,1,...,n-1`. Increment rightmost digit that can increase, reset all digits to its right to be consecutive.

## Step-by-step Algorithm
1. Validate `n` (1 ≤ n ≤ 9)
2. Initialize digits: `digits[i] = '0' + i`
3. Loop:
   a. Print all `n` digits
   b. Check if last combination (all at max)
   c. If not last, print `", "`
   d. Find rightmost incrementable digit
   e. Increment it and reset digits to right

## The Code (with pedagogical comments)
```c
 <unistd.h>  // Include library for system calls

void ft_putchar(char c)  // Helper function: prints one character
{
    write(1, &c, 1);  // Write 1 byte from address of c to stdout
}

void ft_print_combn(int n)  // Function: returns nothing, takes integer n
{
    if (n <= 0 || n > 9)  // Validate: n must be between 1 and 9
        return;  // Exit if n is invalid
    char digits[10];  // Array to hold the n digits
    int i;  // Loop counter
    int last;  // Flag: is this the last combination?

    i = 0;
    while (i < n)  // Initialize digits to 0, 1, 2, ... n-1
    {
        digits[i] = '0' + i;  // Set digit i to character '0' + i
        i++;
    }
    while (1)  // Infinite loop (breaks from inside)
    {
        i = 0;
        while (i < n)  // Print all n digits
            ft_putchar(digits[i++]);  // Write digit and increment
        last = 1;  // Assume this is the last combination
        i = 0;
        while (i < n)  // Check if all digits are at maximum
        {
            if (digits[i] != '9' - (n - 1 - i))  // If digit i can still increase
            { last = 0; break; }  // Not the last combination
            i++;
        }
        if (!last)  // If not the last combination
            write(1, ", ", 2);  // Print comma and space separator
        i = n - 1;  // Start from the rightmost digit
        while (i >= 0 && digits[i] == '9' - (n - 1 - i))  // Find rightmost digit that can increase
            i--;  // Move left while digit is at maximum
        if (i < 0)  // If no digit can increase (all at max)
            break;  // Exit the loop - we're done
        digits[i]++;  // Increment the found digit
        int j = i + 1;  // Reset all digits to the right
        while (j < n)  // For each digit to the right
        {
            digits[j] = digits[j-1] + 1;  // Set to be consecutive after left neighbor
            j++;
        }
    }
}
```

## Line-by-Line Translation
1. `#include <unistd.h>` - Include the library for system calls
2. `void ft_putchar(char c)` - Define a helper function that prints one character
3. `write(1, &c, 1)` - Write 1 byte from the address of c to stdout
4. `void ft_print_combn(int n)` - Define a function that takes the number of digits
5. `if (n <= 0 || n > 9)` - Check if n is outside valid range (1-9)
6. `return` - Exit early if n is invalid
7. `char digits[10]` - Declare an array to hold the n digits
8. `while (i < n)` - Initialize each digit to its position: 0, 1, 2, ...
9. `digits[i] = '0' + i` - Set digit to character '0' plus its index
10. `while (1)` - Start infinite loop to generate combinations
11. `ft_putchar(digits[i++])` - Print all n digits
12. `last = 1` - Assume this is the last combination
13. `while (i < n)` - Check each digit to see if any can increase
14. `if (digits[i] != '9' - (n - 1 - i))` - If digit i has room to increase
15. `last = 0` - Mark as not the last combination
16. `if (!last)` - If not the last combination
17. `write(1, ", ", 2)` - Print the separator
18. `i = n - 1` - Start checking from the rightmost digit
19. `while (i >= 0 && digits[i] == ...)` - Find rightmost digit that can be incremented
20. `digits[i]++` - Increment that digit
21. `digits[j] = digits[j-1] + 1` - Reset the digit to the right to be consecutive

## Common Traps
- ❌ Using `printf` instead of `write`
- ❌ Printing trailing comma after last combination
- ❌ Not validating `n` (must be 1-9)
- ❌ Forgetting to reset digits after increment
- ❌ Off-by-one in maximum digit calculation

## Related Concepts
- 01_Concepts/odometer_algorithm|Odometer Algorithm
- 01_Concepts/lexicographic_order|Lexicographic Order

## Related Exercises
- [[ft_print_comb2]]
- [[ft_putnbr]]

## Propedeuticity
**Prerequisites:** [[ft_putnbr]], [[ft_print_comb2]]
**Unlocks:** Exam-level combinatorics

How does the odometer algorithm work?
::
Start with 0,1,2...
Find rightmost digit that can increase, increment it, reset all digits to the right to be consecutive.
