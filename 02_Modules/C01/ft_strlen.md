---
tags: [C01, flashcard]
---


# ft_strlen

## Navigation
← [[ft_putstr|ft_putstr]] | [[ft_rev_int_tab|Next: ft_rev_int_tab →]]

## What it does
Returns the length of a string (characters before `\0`).

## The Insight
Count characters until null terminator. Classic "invisible skeleton" pattern.

## Step-by-step Algorithm
1. Receive `char *str`
2. Initialize `i = 0`
3. While `str[i] != '\0'`, increment `i`
4. Return `i`

## The Code (with pedagogical comments)
```c
int ft_strlen(char *str)  // Function: returns int, takes string pointer
{
    int i;  // Counter variable

    i = 0;  // Start counting from position 0
    while (str[i] != '\0')  // Loop until we hit the null terminator
        i++;  // Move to next character
    return (i);  // Return the count
}
```

## Line-by-Line Translation
1. `int ft_strlen(char *str)` - Define a function that returns an integer and takes a string pointer
2. `int i` - Declare a counter variable
3. `i = 0` - Start the counter at position 0
4. `while (str[i] != '\0')` - Keep looping while the current character is not the null terminator
5. `i++` - Move to the next character
6. `return (i)` - Return the final count

## Common Traps
- ❌ Forgetting null terminator check
- ❌ Not initializing counter

## Related Concepts
- 01_Concepts/invisible_skeleton|Invisible Skeleton
- 01_Concepts/null_terminator|Null Terminator

## Related Exercises
- [[ft_putstr]]
- [[ft_strcpy]]

## Propedeuticity
**Prerequisites:** [[ft_putstr]]
**Unlocks:** C02 string functions (ft_strcpy, etc.)

What is the "invisible skeleton" pattern?
::
```c
int i = 0;
while (str[i] != '\0')
    i++;
```
