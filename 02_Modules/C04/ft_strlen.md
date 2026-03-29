---
tags: [C04]
---


# ft_strlen

## What it does
Returns the length of a string (number of characters before the null terminator).

## Insight
A string's length is determined by counting characters until the null terminator (`\0`). The function uses a simple loop to increment a counter.

## Algorithm
1. Receive a pointer to a character (`char *str`).
2. Initialize a counter `i` to 0.
3. Loop while `str[i]` is not the null terminator (`\0`).
4. Inside the loop, increment `i`.
5. When the loop ends, return `i`.

## Code (with pedagogical comments)
```c
int ft_strlen(char *str)  // Function: returns the length of the string (characters before '\0')
{
    int i;  // Counter variable to track position in the string

    i = 0;  // Start counting from position 0
    while (str[i] != '\0')  // Keep looping while we haven't reached the null terminator
    {
        i++;  // Increment counter for each character found
    }
    return (i);  // Return the total count (string length)
}
```

## Line-by-Line Translation
1. `int ft_strlen(char *str)` - Define a function that takes a string pointer and returns an integer representing its length
2. `int i;` - Declare an integer variable `i` to use as a position counter
3. `i = 0;` - Initialize the counter to 0, starting at the first character
4. `while (str[i] != '\0')` - Continue looping as long as the current character is NOT the null terminator (meaning we haven't reached the end)
5. `i++;` - Increment i to move to the next character position in the string
6. `return (i);` - After the loop ends (we hit '\0'), return the counter value which equals the number of characters before the null terminator

## Common Traps
- ❌ Forgetting to check for the null terminator (would count past the string).
- ❌ Not initializing `i` to 0 (undefined behavior).
- ❌ Returning a negative value (if `i` is decremented incorrectly).

## Related Concepts
- Null Terminator - The `\0` character that ends strings in C
- Invisible Skeleton - The `while (str[i] != '\0')` pattern
- Memory as Array - Understanding memory as an array of bytes

## Propedeuticity
Foundation for all string manipulation exercises. Required before `ft_strcpy`, `ft_strcmp`, `ft_strdup`, and most C02-C06 exercises.
