---
tags: [C02, flashcard]
---


# ft_strcpy

## Navigation
← [[ft_strlen|ft_strlen]] | [[ft_strncpy|Next: ft_strncpy →]]

## What it does
Copies string `src` to `dest`, including null terminator.

## The Insight
Classic string copy: iterate through src until `\0`, copy each char, then add `\0`.

## Step-by-step Algorithm
1. Initialize `i = 0`
2. While `src[i] != '\0'`: copy and increment
3. Set `dest[i] = '\0'`
4. Return `dest`

## The Code (with pedagogical comments)
```c
char *ft_strcpy(char *dest, char *src)  // Function: returns pointer, takes two string pointers
{
    int i;  // Counter variable

    i = 0;  // Start at position 0
    while (src[i] != '\0')  // Loop until null terminator in source
    {
        dest[i] = src[i];  // Copy character from src to dest
        i++;  // Move to next position
    }
    dest[i] = '\0';  // Add null terminator to dest
    return (dest);  // Return the destination string
}
```

## Line-by-Line Translation
1. `char *ft_strcpy(char *dest, char *src)` - Define a function that returns a string pointer and takes two string pointers
2. `int i` - Declare a counter variable
3. `i = 0` - Start the counter at position 0
4. `while (src[i] != '\0')` - Keep looping while we haven't reached the end of source string
5. `dest[i] = src[i]` - Copy the current character from source to destination
6. `i++` - Move to the next character
7. `dest[i] = '\0'` - Add the null terminator to mark the end of destination string
8. `return (dest)` - Return the destination pointer

## Common Traps
- ❌ Forgetting to null-terminate dest
- ❌ Returning src instead of dest
- ❌ Not copying the null terminator

## Related Concepts
- 01_Concepts/null_terminator|Null Terminator

## Related Exercises
- [[ft_strlen]]
- [[ft_strncpy]]
- [[ft_strlcpy]]

## Propedeuticity
**Prerequisites:** [[ft_strlen]]
**Unlocks:** [[ft_strncpy]], [[ft_strlcpy]]

How do you copy a string?
::
```c
i = 0;
while (src[i]) {
    dest[i] = src[i];
    i++;
}
dest[i] = '\0';
```
