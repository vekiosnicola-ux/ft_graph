---
tags: [Level_3, exam]
  - string-parsing
  - white
Level: 3
Topic: Algorithms
Exercise: ft_atoi_base
---


# ft_atoi_base

## What It Does
Converts a string in a custom base (2-16) to an integer. Supports bases 2 through 16.

## The Insight
Like ft_atoi but with custom digit values. Each digit: `result = result * base + digit_value`. Handles optional negative sign.

## Step-by-Step Algorithm
1. Skip whitespace
2. Check for optional sign
3. For each char: convert to digit value (0-9, A-F, a-f)
4. `result = result * base + digit`
5. Apply sign at end

## Code
```c
int ft_atoi_base(char *str, int base)          // Function: takes string and base, returns int
{
    int i = 0, sign = 1, result = 0;           // i=index, sign=1/-1, result=accumulator

    // Skip leading whitespace
    while (str[i] == ' ' || str[i] == '\t')   // Check for space or tab
        i++;

    // Handle optional sign
    if (str[i] == '-')                         // If minus sign
    {
        sign = -1;                              // Set sign to negative
        i++;                                     // Move past sign character
    }

    // Convert each character to digit value and accumulate
    while (str[i])
    {
        // If digit '0'-'9': value is str[i] - '0'
        if (str[i] >= '0' && str[i] <= '9')
            result = result * base + str[i] - '0';
        // If uppercase 'A'-'F': value is str[i] - '7' (A=10, B=11, etc.)
        else if (str[i] >= 'A' && str[i] <= 'F')
            result = result * base + str[i] - '7';
        // If lowercase 'a'-'f': value is str[i] - 'W' (a=10, b=11, etc.)
        else if (str[i] >= 'a' && str[i] <= 'f')
            result = result * base + str[i] - 'W';
        i++;
    }

    return sign * result;                       // Return result with sign applied
}
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int ft_atoi_base(char *str, int base)` | Define function: takes string and base, returns int |
| `{` | Start of function body |
| `int i = 0, sign = 1, result = 0;` | Initialize index, sign, and result accumulator |
| `while (str[i] == ' '\|\| str[i] == '\t')` | Skip leading whitespace |
| `i++;` | Move past whitespace |
| `if (str[i] == '-')` | Check if negative sign |
| `{` | Start of sign handling |
| `sign = -1;` | Set sign to negative |
| `i++;` | Move past '-' character |
| `}` | End of sign handling |
| `while (str[i])` | Loop through each character |
| `if (str[i] >= '0' && str[i] <= '9')` | If digit character '0'-'9' |
| `result = result * base + str[i] - '0';` | Accumulate: shift left by base, add digit value |
| `else if (str[i] >= 'A' && str[i] <= 'F')` | If uppercase hex 'A'-'F' |
| `result = result * base + str[i] - '7';` | Accumulate with uppercase offset |
| `else if (str[i] >= 'a' && str[i] <= 'f')` | If lowercase hex 'a'-'f' |
| `result = result * base + str[i] - 'W';` | Accumulate with lowercase offset |
| `i++;` | Move to next character |
| `return sign * result;` | Return result with sign applied |
| `}` | End of function |

## Common Traps
- ❌ Not supporting both upper and lowercase hex digits
- ❌ Wrong ASCII offset for A-F (should be '7' for uppercase, 'W' for lowercase)
- ❌ Forgetting to multiply by base each iteration
- ❌ Forgetting to handle sign
- ❌ Not validating that base is between 2 and 16

## Related Exercises
- [[ft_atoi]] - Decimal conversion
- [[print_hex]] - Hexadecimal output

## Wiki Links
03_Exams/Level_3_INDEX|Level 3 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 52 lines)
