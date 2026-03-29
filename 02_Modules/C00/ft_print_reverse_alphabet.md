---
tags: [C00, flashcard]
---


# ft_print_reverse_alphabet

## What it does
Prints the lowercase alphabet from 'z' down to 'a' sequentially.

## The Insight
Same as `ft_print_alphabet` but decrementing instead of incrementing. Characters are integers, so decrementing moves through ASCII in reverse.

## Step-by-step Algorithm
1. Include `<unistd.h>` for `write`
2. Declare `char letter = 'z'`
3. While `letter >= 'a'`, write the character and decrement

## The Code (with pedagogical comments)
```c
 <unistd.h>  // Include library for system calls (write, read, close)

void ft_print_reverse_alphabet(void)  // Function: returns nothing, takes nothing
{
    char letter;  // Variable to hold current character

    letter = 'z';  // Start with lowercase 'z' (ASCII 122)
    while (letter >= 'a')  // Loop until we reach 'a' (ASCII 97)
    {
        write(1, &letter, 1);  // Write 1 byte from address of letter to stdout
        letter--;  // Move to previous character in ASCII table
    }
}
```

## Line-by-Line Translation
1. `#include <unistd.h>` - Include the library for system calls like write()
2. `void ft_print_reverse_alphabet(void)` - Define a function that returns nothing and takes nothing
3. `char letter` - Create a variable to hold the current character
4. `letter = 'z'` - Start with the character 'z' (ASCII value 122)
5. `while (letter >= 'a')` - Keep looping while the character is greater than or equal to 'a'
6. `write(1, &letter, 1)` - Write 1 byte from the address of letter to stdout
7. `letter--` - Move to the previous character in the ASCII table

## Common Traps
- ❌ Using `printf` instead of `write`
- ❌ Forgetting to decrement `letter` (infinite loop)
- ❌ Starting from `'a'` (forward) instead of `'z'`
- ❌ Using `>` instead of `>=` (would skip 'a')

## Related Concepts
- 01_Concepts/ascii_math|ASCII Math
- 01_Concepts/while_loop|While Loop

## Related Exercises
- [[ft_print_alphabet]]
- [[ft_print_numbers]]

## Propedeuticity
**Prerequisites:** [[ft_print_alphabet]]
**Unlocks:** Character arithmetic understanding

How do you print the alphabet in reverse?
::
```c
char letter = 'z';
while (letter >= 'a') {
    write(1, &letter, 1);
    letter--;
}
```
