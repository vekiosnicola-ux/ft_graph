---
tags: [C01, flashcard]
---


# ft_putstr

## Navigation
← [[ft_ultimate_div_mod|ft_ultimate_div_mod]] | [[ft_strlen|Next: ft_strlen →]]

## What it does
Prints a string character by character until `\0`.

## The Insight
Strings are char arrays terminated by `\0`. Iterate and write each character.

## Step-by-step Algorithm
1. Receive `char *str`
2. Initialize `i = 0`
3. While `str[i] != '\0'`:
   a. Write `str[i]`
   b. Increment `i`

## The Code (with pedagogical comments)
```c
void ft_putstr(char *str)  // Function: returns nothing, takes string pointer
{
    int i;  // Counter variable

    i = 0;  // Start at position 0
    while (str[i] != '\0')  // Loop until null terminator
    {
        write(1, &str[i], 1);  // Write 1 byte from address of str[i] to stdout
        i++;  // Move to next character
    }
}
```

## Line-by-Line Translation
1. `void ft_putstr(char *str)` - Define a function that returns nothing and takes a string pointer
2. `int i` - Create a counter variable
3. `i = 0` - Start the counter at position 0
4. `while (str[i] != '\0')` - Keep looping while the current character is not the null terminator
5. `write(1, &str[i], 1)` - Write 1 byte from the address of the current character to stdout
6. `i++` - Move to the next character

## Common Traps
- ❌ Forgetting null terminator check
- ❌ Not incrementing index

## Related Concepts
- 01_Concepts/null_terminator|Null Terminator
- 07_Manual/c_unistd.h|unistd.h

## Related Exercises
- [[ft_strlen]]
- [[ft_strcpy]]

## Propedeuticity
**Prerequisites:** C00 output exercises
**Unlocks:** [[ft_strlen]], C02 string functions

How do you print a string?
::
```c
int i = 0;
while (str[i] != '\0') {
    write(1, &str[i], 1);
    i++;
}
```
