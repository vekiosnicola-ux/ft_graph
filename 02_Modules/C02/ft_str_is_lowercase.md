---
tags: [C02, flashcard]
---


# ft_str_is_lowercase

## What it does
Returns 1 if all characters are lowercase (a-z), else 0.

## The Insight
Check ASCII range: 'a'-'z' (97-122).

## Step-by-step Algorithm
1. Initialize `i = 0`
2. While `str[i] != '\0'`:
   a. If not between 'a' and 'z': return 0
   b. Increment i
3. Return 1

## The Code (with pedagogical comments)
```c
int ft_str_is_lowercase(char *str)  // Function: returns int (0 or 1), takes string pointer
{
    int i;  // Counter variable

    i = 0;  // Start at position 0
    while (str[i] != '\0')  // Loop until null terminator
    {
        if (!(str[i] >= 'a' && str[i] <= 'z'))  // If character is NOT lowercase
            return (0);  // Return 0 (false)
        i++;  // Move to next character
    }
    return (1);  // All characters were lowercase, return 1 (true)
}
```

## Line-by-Line Translation
1. `int ft_str_is_lowercase(char *str)` - Define a function that returns 0 or 1 and takes a string pointer
2. `int i` - Create a counter variable
3. `i = 0` - Start the counter at position 0
4. `while (str[i] != '\0')` - Keep looping while we haven't reached the end of string
5. `if (!(str[i] >= 'a' && str[i] <= 'z'))` - Check if the current character is NOT between 'a' and 'z'
6. `return (0)` - If not lowercase, return 0 immediately
7. `i++` - Move to the next character
8. `return (1)` - If we finished the loop, all characters were lowercase

## Common Traps
- ❌ Using `islower()` from ctype.h (not allowed)
- ❌ Forgetting empty string returns 1
- ❌ Wrong logical operator (should be &&, not ||)

## Related Concepts
- 01_Concepts/ascii_math|ASCII Math
- [[ft_str_is_alpha]]

## Related Exercises
- [[ft_str_is_alpha]]
- [[ft_strlowcase]]

## Propedeuticity
**Prerequisites:** [[ft_str_is_alpha]]
**Unlocks:** [[ft_strlowcase]]

How do you check if a character is lowercase?
::
Check if it's between 'a' and 'z' (ASCII 97-122):
```c
if (str[i] >= 'a' && str[i] <= 'z')
```
