---
tags: [C00, flashcard]
---


# ft_print_comb

## Navigation
← [[ft_is_negative|ft_is_negative]] | [[ft_print_comb2|Next: ft_print_comb2 →]]

## What it does
Prints all unique three-digit combinations of digits (0-9) in ascending order, separated by comma and space, with no trailing comma.

## The Insight
Three nested loops where each digit is strictly greater than the previous (`i < j < k`). This ensures each combination appears exactly once in sorted order.

## Step-by-step Algorithm
1. Loop `i` from `'0'` to `'7'`
2. Set `j = i + 1`, loop `j` from `i+1` to `'8'`
3. Set `k = j + 1`, loop `k` from `j+1` to `'9'`
4. Write `i`, `j`, `k`
5. If not last combination, write `", "`

## The Code (with pedagogical comments)
```c
 <unistd.h>  // Include library for system calls

void    ft_print_comb(void)  // Function: returns nothing, takes nothing
{
    char    i;  // First digit of combination
    char    j;  // Second digit of combination
    char    k;  // Third digit of combination

    i = '0';  // Start first digit at '0'
    while (i <= '7')  // First digit goes up to '7' (need room for j and k)
    {
        j = i + 1;  // Second digit starts one after first
        while (j <= '8')  // Second digit goes up to '8' (need room for k)
        {
            k = j + 1;  // Third digit starts one after second
            while (k <= '9')  // Third digit goes up to '9'
            {
                write(1, &i, 1);  // Write first digit
                write(1, &j, 1);  // Write second digit
                write(1, &k, 1);  // Write third digit
                if (!(i == '7' && j == '8' && k == '9'))  // If not last combination
                    write(1, ", ", 2);  // Write comma and space
                k++;  // Move to next third digit
            }
            j++;  // Move to next second digit
        }
        i++;  // Move to next first digit
    }
}
```

## Line-by-Line Translation
1. `#include <unistd.h>` - Include the library for system calls
2. `void ft_print_comb(void)` - Define a function that returns nothing and takes nothing
3. `char i, j, k` - Create three variables for the three digits
4. `i = '0'` - Start the first digit at '0'
5. `while (i <= '7')` - Loop while first digit is at most '7'
6. `j = i + 1` - Set second digit to one more than first
7. `while (j <= '8')` - Loop while second digit is at most '8'
8. `k = j + 1` - Set third digit to one more than second
9. `while (k <= '9')` - Loop while third digit is at most '9'
10. `write(1, &i, 1)` - Write the first digit
11. `write(1, &j, 1)` - Write the second digit
12. `write(1, &k, 1)` - Write the third digit
13. `if (!(i == '7' && j == '8' && k == '9'))` - Check if this is NOT the last combination
14. `write(1, ", ", 2)` - Write comma and space separator
15. `k++` - Move to next third digit
16. `j++` - Move to next second digit
17. `i++` - Move to next first digit

## Common Traps
- ❌ Using `printf` instead of `write`
- ❌ Printing trailing comma after last combination
- ❌ Starting loops from `'0'` to `'9'` without ensuring `i < j < k`
- ❌ Forgetting to increment loop variables

## Related Concepts
- 01_Concepts/ascii_math|ASCII Math

## Related Exercises
- [[ft_print_numbers]]
- [[ft_print_comb2]]
- [[ft_print_combn]]

## Propedeuticity
**Prerequisites:** [[ft_print_numbers]]
**Unlocks:** [[ft_print_comb2]], [[ft_print_combn]]

How do you print all 3-digit combinations?
::
Use 3 nested loops where each digit is greater than the previous: i < j < k
