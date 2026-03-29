---
tags: [Level_2, exam]
Level: 2
Topic: String Manipulation
Exercise: ft_atoi
---


# ft_atoi

## What It Does
Converts a string to an integer. The string may have leading whitespace, an optional sign (+ or -), and then digits. The conversion stops at the first non-digit character.

## The Insight
This teaches you how to parse numeric strings. The key insight is:
1. Skip leading whitespace (space, tab, newline, etc.)
2. Check for an optional sign (+ or -)
3. Convert each digit character to its numeric value and accumulate: `result = result * 10 + digit`
4. Stop when a non-digit is encountered
5. Apply the sign

## Step-by-Step Algorithm
1. Initialize index `i = 0`, `sign = 1`, `result = 0`
2. Skip whitespace: while `str[i]` is space, tab, newline, etc.
3. Check for sign: if `str[i]` is '-', `sign = -1` and increment `i`
4. While `str[i]` is a digit ('0' to '9'):
   - Convert char to digit: `digit = str[i] - '0'`
   - Update result: `result = result * 10 + digit`
   - Increment `i`
5. Return `sign * result`

## Code
```c
 <unistd.h>                                 // Include header for write() (not directly used here but standard)

int ft_atoi(char *str)                             // Function: takes string, returns integer
{
    int i = 0;                                      // Index for traversing the string
    int sign = 1;                                   // Sign multiplier: 1 for positive, -1 for negative
    int result = 0;                                 // Accumulated numeric result

    // Skip leading whitespace characters
    while (str[i] == ' ' || str[i] == '\t' || str[i] == '\n' ||  // While char is common whitespace
           str[i] == '\v' || str[i] == '\f' || str[i] == '\r')
        i++;                                        // Move past whitespace characters

    // Handle optional sign character
    if (str[i] == '-')                             // If minus sign encountered
    {
        sign = -1;                                  // Set sign to negative
        i++;                                        // Move past the '-' character
    }
    else if (str[i] == '+')                        // If plus sign encountered
        i++;                                        // Move past '+' (sign stays +1)

    // Convert digit characters to numeric value
    while (str[i] >= '0' && str[i] <= '9')         // While current char is a digit
    {
        result = result * 10 + (str[i] - '0');      // Accumulate: shift previous digits left, add new digit
        i++;                                        // Move to next character
    }

    return (sign * result);                         // Return result with sign applied
}
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `#include <unistd.h>` | Include header for write() syscall |
| `int ft_atoi(char *str)` | Define function: takes string pointer, returns integer |
| `{` | Start of function body |
| `int i = 0;` | Initialize string index to 0 |
| `int sign = 1;` | Initialize sign multiplier to positive |
| `int result = 0;` | Initialize result accumulator to 0 |
| `while (str[i] == ' ' \|\| ...)` | Skip all common whitespace characters |
| `i++;` | Move past whitespace |
| `if (str[i] == '-')` | Check if negative sign encountered |
| `{` | Start of negative sign block |
| `sign = -1;` | Set sign to negative |
| `i++;` | Move past '-' character |
| `}` | End of negative sign block |
| `else if (str[i] == '+')` | Check if explicit positive sign |
| `i++;` | Move past '+' character |
| `while (str[i] >= '0' && str[i] <= '9')` | Loop while current char is a digit |
| `{` | Start of conversion loop body |
| `result = result * 10 + (str[i] - '0');` | Accumulate: shift previous digits left, add new digit |
| `i++;` | Move to next character |
| `}` | End of conversion loop body |
| `return (sign * result);` | Return result with sign applied |
| `}` | End of function |

## Common Traps
- ❌ Forgetting to skip whitespace
- ❌ Mishandling the sign (e.g., forgetting to increment `i` after sign)
- ❌ Overflow (not required to handle in basic exercises)
- ❌ Using wrong digit conversion (should be `str[i] - '0'`)
- ❌ Not stopping at non-digit
- ❌ Forgetting to apply the sign at the end

## Related Exercises
- [[do_op]] - Uses ft_atoi to parse operands
- [[print_hex]] - Uses atoi and base conversion
- [[ft_atoi_base]] - Custom base conversion

## Wiki Links
03_Exams/Level_2_INDEX|Level 2 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 112 lines)
