---
tags: [C02, flashcard]
---


# ft_strlcpy

## What it does
Copies `size - 1` chars from src to dest, null-terminates dest, returns src length.

## The Insight
Unlike strncpy, guarantees null termination and returns src length for truncation detection.

## Step-by-step Algorithm
1. Compute len = strlen(src)
2. If size == 0, return len
3. Copy min(len, size-1) chars
4. Null-terminate dest
5. Return len

## The Code (with pedagogical comments)
```c
unsigned int ft_strlcpy(char *dest, char *src, unsigned int size)  // Function: returns length, takes dest, src, size
{
    unsigned int i;  // Counter variable
    unsigned int len;  // Length of source string

    len = 0;
    while (src[len] != '\0')  // First, calculate the length of src
        len++;
    i = 0;
    if (size == 0)  // If size is 0, only return the length (nothing to copy)
        return (len);
    while (src[i] != '\0' && i < size - 1)  // Copy up to size-1 characters
    {
        dest[i] = src[i];  // Copy character from src to dest
        i++;  // Move to next position
    }
    dest[i] = '\0';  // Always null-terminate (if size > 0)
    return (len);  // Return the original length of src
}
```

## Line-by-Line Translation
1. `unsigned int ft_strlcpy(char *dest, char *src, unsigned int size)` - Define a function that returns src length and takes dest, src, and buffer size
2. `unsigned int i, len` - Declare counter and length variables
3. `while (src[len] != '\0')` - Calculate length of source string
4. `len++` - Count each character
5. `i = 0` - Reset counter for copying
6. `if (size == 0)` - If buffer size is 0
7. `return (len)` - Return length without copying anything
8. `while (src[i] != '\0' && i < size - 1)` - Copy while src has chars AND we haven't filled the buffer
9. `dest[i] = src[i]` - Copy one character
10. `i++` - Move to next position
11. `dest[i] = '\0'` - Always null-terminate the destination
12. `return (len)` - Return the original source length

## Common Traps
- ❌ Forgetting to null-terminate when size > 0
- ❌ Not returning src length (should always return original length)
- ❌ Off-by-one: copy size-1, not size

## Related Concepts
- 01_Concepts/null_terminator|Null Terminator
- [[ft_strncpy]]

## Related Exercises
- [[ft_strncpy]]
- [[ft_strcpy]]

## Propedeuticity
**Prerequisites:** [[ft_strncpy]]
**Unlocks:** C03 string functions

How is ft_strlcpy safer than strncpy?
::
1. Always null-terminates (if size > 0)
2. Returns src length for truncation detection
3. Copies size-1 bytes, not size
