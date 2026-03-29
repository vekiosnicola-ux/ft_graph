---
tags: [C02, flashcard]
---


# ft_strupcase

## What it does
Converts all lowercase letters to uppercase.

## The Insight
Lowercase letters are 32 positions after uppercase in ASCII. Subtract 32 to uppercase.

## Step-by-step Algorithm
1. Initialize `i = 0`
2. While `str[i] != '\0'`:
   a. If between 'a' and 'z': subtract 32
   b. Increment i
3. Return `str`

## The Code (with pedagogical comments)
```c
char *ft_strupcase(char *str)  // Function: returns string pointer, takes string pointer
{
    int i;  // Counter variable

    i = 0;  // Start at position 0
    while (str[i] != '\0')  // Loop until null terminator
    {
        if (str[i] >= 'a' && str[i] <= 'z')  // If character is lowercase
            str[i] = str[i] - 32;  // Convert to uppercase (subtract 32 from ASCII)
        i++;  // Move to next character
    }
    return (str);  // Return the modified string
}
```

## Line-by-Line Translation
1. `char *ft_strupcase(char *str)` - Define a function that returns a string pointer and takes a string pointer
2. `int i` - Create a counter variable
3. `i = 0` - Start the counter at position 0
4. `while (str[i] != '\0')` - Keep looping while we haven't reached the end of string
5. `if (str[i] >= 'a' && str[i] <= 'z')` - Check if the current character is lowercase
6. `str[i] = str[i] - 32` - Convert to uppercase by subtracting 32 from ASCII value
7. `i++` - Move to the next character
8. `return (str)` - Return the modified string

## Common Traps
- ❌ Using `toupper()` from ctype.h (not allowed)
- ❌ Modifying non-lowercase characters (should only modify 'a'-'z')
- ❌ Forgetting to return str

## Related Concepts
- 01_Concepts/ascii_math|ASCII Math
- [[ft_strlowcase]]

## Related Exercises
- [[ft_str_is_uppercase]]
- [[ft_strcapitalize]]

## Propedeuticity
**Prerequisites:** [[ft_str_is_uppercase]]
**Unlocks:** [[ft_strcapitalize]]

How do you convert lowercase to uppercase?
::
Subtract 32 from the ASCII value (or use `'a' - 'A'`):
```c
str[i] = str[i] - 32;  // 'a'(97) - 32 = 'A'(65)
```
