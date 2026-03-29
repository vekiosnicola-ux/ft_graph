---
tags: [C02, flashcard]
---


# ft_str_is_numeric

## What it does
Returns 1 if all characters are digits (0-9), else 0.

## The Insight
Check ASCII range for digits: '0'-'9' (48-57).

## Step-by-step Algorithm
1. Initialize `i = 0`
2. While `str[i] != '\0'`:
   a. If not between '0' and '9': return 0
   b. Increment i
3. Return 1

## The Code (with pedagogical comments)
```c
int ft_str_is_numeric(char *str)  // Function: returns int (0 or 1), takes string pointer
{
    int i;  // Counter variable

    i = 0;  // Start at position 0
    while (str[i] != '\0')  // Loop until null terminator
    {
        if (!(str[i] >= '0' && str[i] <= '9'))  // If character is NOT a digit
            return (0);  // Return 0 (false)
        i++;  // Move to next character
    }
    return (1);  // All characters were digits, return 1 (true)
}
```

## Line-by-Line Translation
1. `int ft_str_is_numeric(char *str)` - Define a function that returns 0 or 1 and takes a string pointer
2. `int i` - Create a counter variable
3. `i = 0` - Start the counter at position 0
4. `while (str[i] != '\0')` - Keep looping while we haven't reached the end of string
5. `if (!(str[i] >= '0' && str[i] <= '9'))` - Check if the current character is NOT between '0' and '9'
6. `return (0)` - If not a digit, return 0 immediately
7. `i++` - Move to the next character
8. `return (1)` - If we finished the loop, all characters were digits

## Common Traps
- ❌ Using `isdigit()` from ctype.h (not allowed)
- ❌ Forgetting empty string returns 1
- ❌ Wrong logical operator (should be &&, not ||)

## Related Concepts
- 01_Concepts/ascii_math|ASCII Math
- [[ft_str_is_alpha]]

## Related Exercises
- [[ft_str_is_alpha]]
- [[ft_atoi]] (C04)

## Propedeuticity
**Prerequisites:** [[ft_str_is_alpha]]
**Unlocks:** C04 atoi exercises

How do you check if a character is a digit?
::
Check if it's between '0' and '9' (ASCII 48-57):
```c
if (str[i] >= '0' && str[i] <= '9')
```
