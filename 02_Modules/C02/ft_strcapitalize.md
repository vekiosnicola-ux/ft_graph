---
tags: [C02, flashcard]
---


# ft_strcapitalize

## What it does
Capitalizes first letter of each word, lowercases rest.

## The Insight
Word start = first char OR previous char is NOT lowercase letter. Uppercase at word start, lowercase otherwise.

## Step-by-step Algorithm
1. Initialize `i = 0`
2. While `str[i] != '\0'`:
   a. If `i == 0` OR `str[i-1]` not lowercase:
      - If lowercase: uppercase
   b. Else: if uppercase: lowercase
   c. Increment i
3. Return `str`

## The Code (with pedagogical comments)
```c
char *ft_strcapitalize(char *str)  // Function: returns string pointer, takes string pointer
{
    int i;  // Counter variable

    i = 0;  // Start at position 0
    while (str[i] != '\0')  // Loop until null terminator
    {
        if (i == 0 || !(str[i-1] >= 'a' && str[i-1] <= 'z'))  // If at word start (first char or prev not lowercase)
        {
            if (str[i] >= 'a' && str[i] <= 'z')  // If lowercase
                str[i] = str[i] - 32;  // Convert to uppercase
        }
        else if (str[i] >= 'A' && str[i] <= 'Z')  // Else if uppercase
            str[i] = str[i] + 32;  // Convert to lowercase
        i++;  // Move to next character
    }
    return (str);  // Return the modified string
}
```

## Line-by-Line Translation
1. `char *ft_strcapitalize(char *str)` - Define a function that returns a string pointer and takes a string pointer
2. `int i` - Create a counter variable
3. `i = 0` - Start the counter at position 0
4. `while (str[i] != '\0')` - Keep looping while we haven't reached the end of string
5. `if (i == 0 || !(str[i-1] >= 'a' && str[i-1] <= 'z'))` - Check if at word start (first char OR previous not lowercase)
6. `if (str[i] >= 'a' && str[i] <= 'z')` - If the current character is lowercase
7. `str[i] = str[i] - 32` - Convert to uppercase
8. `else if (str[i] >= 'A' && str[i] <= 'Z')` - Else if the current character is uppercase
9. `str[i] = str[i] + 32` - Convert to lowercase
10. `i++` - Move to the next character
11. `return (str)` - Return the modified string

## Common Traps
- ❌ Wrong condition for "word start" (must check if previous is NOT lowercase)
- ❌ Forgetting to lowercase inside words
- ❌ Off-by-one at i == 0 (str[i-1] doesn't exist, but i == 0 handles it)

## Related Concepts
- 01_Concepts/ascii_math|ASCII Math
- [[ft_strupcase]]
- [[ft_strlowcase]]

## Related Exercises
- [[ft_strupcase]]
- [[ft_strlowcase]]

## Propedeuticity
**Prerequisites:** [[ft_strupcase]], [[ft_strlowcase]]
**Unlocks:** C03 string functions

What defines a "word start" in ft_strcapitalize?
::
First character of string (i == 0) OR previous character is NOT a lowercase letter.
