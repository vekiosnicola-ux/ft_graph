---
tags: [C02, flashcard]
---


# ft_str_is_alpha

## Navigation
← [[ft_strcpy|ft_strcpy]] | [[ft_str_is_numeric|Next: ft_str_is_numeric →]]

## What it does
Returns 1 if all characters are alphabetic (A-Z or a-z), else 0.

## The Insight
Check ASCII ranges: 'A'-'Z' (65-90), 'a'-'z' (97-122).

## Step-by-step Algorithm
1. Initialize `i = 0`
2. While `str[i] != '\0'`:
   a. If not between A-Z AND not between a-z: return 0
   b. Increment i
3. Return 1

## The Code (with pedagogical comments)
```c
int ft_str_is_alpha(char *str)  // Function: returns int (0 or 1), takes string pointer
{
    int i;  // Counter variable

    i = 0;  // Start at position 0
    while (str[i] != '\0')  // Loop until null terminator
    {
        if (!((str[i] >= 'A' && str[i] <= 'Z') || (str[i] >= 'a' && str[i] <= 'z')))
            return (0);  // If character is NOT alphabetic, return 0
        i++;  // Move to next character
    }
    return (1);  // All characters were alphabetic, return 1
}
```

## Line-by-Line Translation
1. `int ft_str_is_alpha(char *str)` - Define a function that returns 0 or 1 and takes a string pointer
2. `int i` - Create a counter variable
3. `i = 0` - Start the counter at position 0
4. `while (str[i] != '\0')` - Keep looping while we haven't reached the end of string
5. `if (!((str[i] >= 'A' && str[i] <= 'Z') || (str[i] >= 'a' && str[i] <= 'z')))` - Check if the current character is NOT uppercase AND NOT lowercase
6. `return (0)` - If not alphabetic, return 0 immediately
7. `i++` - Move to the next character
8. `return (1)` - If we finished the loop, all characters were alphabetic

## Common Traps
- ❌ Using `isalpha()` from ctype.h (not allowed)
- ❌ Forgetting empty string returns 1
- ❌ Wrong logical operator (AND vs OR)

## Related Concepts
- 01_Concepts/ascii_math|ASCII Math
- 07_Manual/c_ctype.h|ctype.h

## Related Exercises
- [[ft_str_is_numeric]]
- [[ft_str_is_lowercase]]
- [[ft_str_is_uppercase]]

## Propedeuticity
**Prerequisites:** [[ft_strlen]]
**Unlocks:** [[ft_strcapitalize]]

How do you check if a character is alphabetic?
::
Check if it's between 'A'-'Z' OR between 'a'-'z'
