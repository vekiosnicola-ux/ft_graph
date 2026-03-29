---
tags: [C00, flashcard]
---


# ft_print_alphabet

## Navigation
← [[ft_putchar|ft_putchar]] | [[ft_print_reverse_alphabet|Next: ft_print_reverse_alphabet →]]

## What it does
Prints the lowercase alphabet from 'a' to 'z' sequentially.

## The Insight
Characters in C are integers (ASCII values). Incrementing a `char` from `'a'` to `'z'` walks through consecutive ASCII codes.

## Step-by-step Algorithm
1. Include `<unistd.h>` for `write`
2. Declare `char letter = 'a'`
3. While `letter <= 'z'`, write the character and increment

## The Code (with pedagogical comments)
```c
 <unistd.h>  // Include library for system calls (write, read, close)

void    ft_print_alphabet(void)  // Function: returns nothing, takes nothing
{
    char    letter;  // Variable to hold current character

    letter = 'a';  // Start with lowercase 'a' (ASCII 97)
    while (letter <= 'z')  // Loop until we reach 'z' (ASCII 122)
    {
        write(1, &letter, 1);  // Write 1 byte from address of letter to stdout
        letter++;  // Move to next character in ASCII table
    }
}
```

## Line-by-Line Translation
1. `#include <unistd.h>` - Include the library for system calls like write()
2. `void ft_print_alphabet(void)` - Define a function that returns nothing and takes nothing
3. `char letter` - Create a variable to hold the current character
4. `letter = 'a'` - Start with the character 'a' (ASCII value 97)
5. `while (letter <= 'z')` - Keep looping while the character is less than or equal to 'z'
6. `write(1, &letter, 1)` - Write 1 byte from the address of letter to stdout
7. `letter++` - Move to the next character in the ASCII table

## Common Traps
- ❌ Using `printf` instead of `write`
- ❌ Forgetting to increment `letter` (infinite loop)
- ❌ Starting from `'A'` (uppercase) instead of `'a'`
- ❌ Using `int` instead of `char`

## Related Concepts
- 01_Concepts/ascii_math|ASCII Math
- 07_Manual/c_unistd.h|unistd.h

## Related Exercises
- [[ft_putchar]]
- [[ft_print_reverse_alphabet]]
- [[ft_print_numbers]]

## Propedeuticity
**Prerequisites:** [[ft_putchar]]
**Unlocks:** [[ft_print_reverse_alphabet]], [[ft_print_numbers]]

How do you print the alphabet?
::
```c
char letter = 'a';
while (letter <= 'z') {
    write(1, &letter, 1);
    letter++;
}
```
