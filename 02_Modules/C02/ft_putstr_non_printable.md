---
tags: [C02, flashcard]
---


# ft_putstr_non_printable

## What it does
Prints string, replacing non-printable chars (<32 or >126) with `\xHH` hex.

## The Insight
Use lookup table for hex conversion. Non-printable = backslash + 2 hex digits.

## Step-by-step Algorithm
1. Iterate through string
2. If printable (32-126): write directly
3. Else: write `\`, hex high nibble, hex low nibble

## The Code (with pedagogical comments)
```c
void ft_putstr_non_printable(char *str)  // Function: returns nothing, takes string pointer
{
    int i;  // Counter variable

    i = 0;  // Start at position 0
    while (str[i] != '\0')  // Loop until null terminator
    {
        if (str[i] >= 32 && str[i] <= 126)  // If character is printable (ASCII 32-126)
            write(1, &str[i], 1);  // Write it directly
        else  // If non-printable
        {
            char buf[3];  // Buffer for "\xHH" format
            buf[0] = '\\';  // Backslash character
            buf[1] = "0123456789abcdef"[str[i] / 16];  // High nibble (first hex digit)
            buf[2] = "0123456789abcdef"[str[i] % 16];  // Low nibble (second hex digit)
            write(1, buf, 3);  // Write the "\xHH" representation
        }
        i++;  // Move to next character
    }
}
```

## Line-by-Line Translation
1. `void ft_putstr_non_printable(char *str)` - Define a function that returns nothing and takes a string pointer
2. `int i` - Create a counter variable
3. `i = 0` - Start the counter at position 0
4. `while (str[i] != '\0')` - Keep looping while we haven't reached the end of string
5. `if (str[i] >= 32 && str[i] <= 126)` - Check if the character is printable
6. `write(1, &str[i], 1)` - If printable, write it directly to stdout
7. `char buf[3]` - If not printable, create a 3-byte buffer
8. `buf[0] = '\\'` - First byte is the backslash
9. `buf[1] = "012345..."[str[i] / 16]` - Second byte is the high hex digit (divide by 16)
10. `buf[2] = "012345..."[str[i] % 16]` - Third byte is the low hex digit (modulo 16)
11. `write(1, buf, 3)` - Write the 3-byte hex representation
12. `i++` - Move to the next character

## Common Traps
- ❌ Using printf/putchar (not allowed; must use write)
- ❌ Negative char values (should cast to unsigned char before division)
- ❌ Forgetting the backslash before hex digits

## Related Concepts
- 01_Concepts/hex_conversion|Hex Conversion
- [[ft_str_is_printable]]

## Related Exercises
- [[ft_str_is_printable]]
- [[ft_print_memory]]

## Propedeuticity
**Prerequisites:** [[ft_str_is_printable]]
**Unlocks:** Exam-level hex questions

How do you convert a byte to hex?
::
Divide by 16 for high nibble, modulo 16 for low nibble:
```c
"0123456789abcdef"[byte / 16]  // High hex digit
"0123456789abcdef"[byte % 16]  // Low hex digit
```
