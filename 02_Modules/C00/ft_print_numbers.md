---
tags: [C00, flashcard]
---


# ft_print_numbers

## What it does
Prints the digits from '0' to '9' sequentially.

## The Insight
Characters `'0'` through `'9'` are consecutive in ASCII (48-57). Incrementing a char variable walks through digit characters.

## Step-by-step Algorithm
1. Include `<unistd.h>` for `write`
2. Declare `char digit = '0'`
3. While `digit <= '9'`, write the character and increment

## The Code (with pedagogical comments)
```c
 <unistd.h>  // Include library for system calls (write, read, close)

void ft_print_numbers(void)  // Function: returns nothing, takes nothing
{
    char digit;  // Variable to hold current digit

    digit = '0';  // Start with character '0' (ASCII 48)
    while (digit <= '9')  // Loop until we reach '9' (ASCII 57)
    {
        write(1, &digit, 1);  // Write 1 byte from address of digit to stdout
        digit++;  // Move to next digit character in ASCII table
    }
}
```

## Line-by-Line Translation
1. `#include <unistd.h>` - Include the library for system calls like write()
2. `void ft_print_numbers(void)` - Define a function that returns nothing and takes nothing
3. `char digit` - Create a variable to hold the current digit character
4. `digit = '0'` - Start with the character '0' (ASCII value 48)
5. `while (digit <= '9')` - Keep looping while the character is less than or equal to '9'
6. `write(1, &digit, 1)` - Write 1 byte from the address of digit to stdout
7. `digit++` - Move to the next digit character in the ASCII table

## Common Traps
- ❌ Using `printf` instead of `write`
- ❌ Forgetting to increment `digit` (infinite loop)
- ❌ Starting from `'1'` instead of `'0'`
- ❌ Using `int` variable but printing as char

## Related Concepts
- 01_Concepts/ascii_math|ASCII Math
- 01_Concepts/while_loop|While Loop

## Related Exercises
- [[ft_print_alphabet]]
- [[ft_putnbr]]

## Propedeuticity
**Prerequisites:** [[ft_print_alphabet]]
**Unlocks:** [[ft_putnbr]]

How do you print digits 0-9?
::
```c
char digit = '0';
while (digit <= '9') {
    write(1, &digit, 1);
    digit++;
}
```
