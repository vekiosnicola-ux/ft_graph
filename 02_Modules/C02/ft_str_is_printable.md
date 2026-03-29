---
tags: [C02, flashcard]
---


# ft_str_is_printable

## What it does
Returns 1 if all characters are printable (ASCII 32-126), else 0.

## The Insight
Printable range: space (32) through tilde (126).

## Step-by-step Algorithm
1. Initialize `i = 0`
2. While `str[i] != '\0'`:
   a. If not between 32 and 126: return 0
   b. Increment i
3. Return 1

## The Code (with pedagogical comments)
```c
int ft_str_is_printable(char *str)  // Function: returns int (0 or 1), takes string pointer
{
    int i;  // Counter variable

    i = 0;  // Start at position 0
    while (str[i] != '\0')  // Loop until null terminator
    {
        if (!(str[i] >= 32 && str[i] <= 126))  // If character is NOT printable (ASCII 32-126)
            return (0);  // Return 0 (false)
        i++;  // Move to next character
    }
    return (1);  // All characters were printable, return 1 (true)
}
```

## Line-by-Line Translation
1. `int ft_str_is_printable(char *str)` - Define a function that returns 0 or 1 and takes a string pointer
2. `int i` - Create a counter variable
3. `i = 0` - Start the counter at position 0
4. `while (str[i] != '\0')` - Keep looping while we haven't reached the end of string
5. `if (!(str[i] >= 32 && str[i] <= 126))` - Check if the current character is NOT between ASCII 32 and 126
6. `return (0)` - If not printable, return 0 immediately
7. `i++` - Move to the next character
8. `return (1)` - If we finished the loop, all characters were printable

## Common Traps
- ❌ Using `isprint()` from ctype.h (not allowed)
- ❌ Forgetting empty string returns 1
- ❌ Off-by-one in range check (must include 32 and 126)

## Related Concepts
- 01_Concepts/ascii_math|ASCII Math
- [[ft_str_is_alpha]]

## Related Exercises
- [[ft_str_is_uppercase]]
- [[ft_putstr_non_printable]]

## Propedeuticity
**Prerequisites:** [[ft_str_is_uppercase]]
**Unlocks:** [[ft_putstr_non_printable]]

What is the printable ASCII range?
::
ASCII 32 (space) through ASCII 126 (tilde).
