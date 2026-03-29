---
tags: [C00, flashcard]
---


# ft_is_negative

## What it does
Prints 'N' if the given integer is negative, otherwise prints 'P'.

## The Insight
Simple conditional logic. Zero is not negative (prints 'P'). Function writes directly to stdout, doesn't return a value.

## Step-by-step Algorithm
1. Include `<unistd.h>` for `write`
2. Declare `char c`
3. If `n < 0`, set `c = 'N'`; else `c = 'P'`
4. Write `c`

## The Code (with pedagogical comments)
```c
 <unistd.h>  // Include library for system calls (write, read, close)

void ft_is_negative(int n)  // Function: returns nothing, takes an integer
{
    char c;  // Variable to hold the output character

    if (n < 0)  // Check if the number is negative
        c = 'N';  // If negative, set output to 'N'
    else  // If positive or zero
        c = 'P';  // Set output to 'P'
    write(1, &c, 1);  // Write the character to stdout
}
```

## Line-by-Line Translation
1. `#include <unistd.h>` - Include the library for system calls like write()
2. `void ft_is_negative(int n)` - Define a function that returns nothing and takes an integer
3. `char c` - Create a variable to hold the output character
4. `if (n < 0)` - Check if the input number is less than zero
5. `c = 'N'` - If negative, assign 'N' to the output character
6. `else` - If the number is zero or positive
7. `c = 'P'` - Assign 'P' to the output character
8. `write(1, &c, 1)` - Write the output character to stdout

## Common Traps
- ❌ Using `printf` instead of `write`
- ❌ Forgetting to write the character (just assigning `c`)
- ❌ Using `else if` for zero (zero is not negative, so 'P')
- ❌ Writing 'N' and 'P' as separate writes

## Related Concepts
- 01_Concepts/conditional|Conditional
- 01_Concepts/write_syscall|write() syscall

## Related Exercises
- [[ft_print_numbers]]
- [[ft_putnbr]]

## Propedeuticity
**Prerequisites:** [[ft_print_numbers]]
**Unlocks:** [[ft_putnbr]]

How do you check if a number is negative?
::
```c
if (n < 0)
    write(1, "N", 1);
else
    write(1, "P", 1);
```
