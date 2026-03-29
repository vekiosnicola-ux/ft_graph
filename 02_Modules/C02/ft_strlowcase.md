---
tags: [C02, flashcard]
---


# ft_strlowcase

## What it does
Converts all uppercase letters to lowercase.

## The Insight
Uppercase letters are 32 positions before lowercase in ASCII. Add 32 to lowercase.

## Step-by-step Algorithm
1. Initialize `i = 0`
2. While `str[i] != '\0'`:
   a. If between 'A' and 'Z': add 32
   b. Increment i
3. Return `str`

## The Code (with pedagogical comments)
```c
char *ft_strlowcase(char *str)  // Function: returns string pointer, takes string pointer
{
    int i;  // Counter variable

    i = 0;  // Start at position 0
    while (str[i] != '\0')  // Loop until null terminator
    {
        if (str[i] >= 'A' && str[i] <= 'Z')  // If character is uppercase
            str[i] = str[i] + 32;  // Convert to lowercase (add 32 to ASCII)
        i++;  // Move to next character
    }
    return (str);  // Return the modified string
}
```

## Line-by-Line Translation
1. `char *ft_strlowcase(char *str)` - Define a function that returns a string pointer and takes a string pointer
2. `int i` - Create a counter variable
3. `i = 0` - Start the counter at position 0
4. `while (str[i] != '\0')` - Keep looping while we haven't reached the end of string
5. `if (str[i] >= 'A' && str[i] <= 'Z')` - Check if the current character is uppercase
6. `str[i] = str[i] + 32` - Convert to lowercase by adding 32 to ASCII value
7. `i++` - Move to the next character
8. `return (str)` - Return the modified string

## Common Traps
- ❌ Using `tolower()` from ctype.h (not allowed)
- ❌ Modifying non-uppercase characters (should only modify 'A'-'Z')
- ❌ Forgetting to return str

## Related Concepts
- 01_Concepts/ascii_math|ASCII Math
- [[ft_strupcase]]

## Related Exercises
- [[ft_str_is_lowercase]]
- [[ft_strcapitalize]]

## Propedeuticity
**Prerequisites:** [[ft_str_is_lowercase]]
**Unlocks:** [[ft_strcapitalize]]

How do you convert uppercase to lowercase?
::
Add 32 to the ASCII value (or use `'a' - 'A'`):
```c
str[i] = str[i] + 32;  // 'A'(65) + 32 = 'a'(97)
```
