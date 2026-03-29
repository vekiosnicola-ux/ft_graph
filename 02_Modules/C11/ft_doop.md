---
tags: []
date: 2026-03-29
status: complete
---
# ft_doop

---
tags: [C11, red]
---

## Navigation
← C11_INDEX|C11 INDEX | [[ft_sort_params|Next: ft_sort_params →]]

## What it does
Performs an operation (`+`, `-`, `*`, `/`, `%`) on two numbers given as strings.

## Step-by-step Algorithm
1. Convert `av[1]` and `av[3]` to integers using `ft_atoi`.
2. Check `av[2]` operator:
   - `+`: return `a + b`
   - `-`: return `a - b`
   - `*`: return `a * b`
   - `/`: return `a / b` (check for division by zero)
   - `%`: return `a % b` (check for modulo by zero)
3. Print the result with `ft_putnbr`.

## The Code
```c
 <unistd.h>  // Provides write() for output

int ft_atoi(char *str);      // Forward declaration: convert string to int
void ft_putnbr(int nb);       // Forward declaration: print integer

int main(int argc, char **argv)  // argc = argument count, argv = arguments array
{
    int a;      // First operand (left side of operator)
    int b;      // Second operand (right side of operator)
    int result; // Stores computed result

    if (argc != 4)  // Expect exactly: program, num1, operator, num2
        return (0);  // Wrong number of arguments; exit quietly
    a = ft_atoi(argv[1]);  // Convert first number string to integer
    b = ft_atoi(argv[3]);  // Convert second number string to integer
    // Check which operator was provided (argv[2])
    if (argv[2][0] == '+')  // Addition: check if first char is '+'
        result = a + b;  // Compute sum
    else if (argv[2][0] == '-')  // Subtraction
        result = a - b;  // Compute difference
    else if (argv[2][0] == '*')  // Multiplication
        result = a * b;  // Compute product
    else if (argv[2][0] == '/')  // Division
    {
        if (b == 0)  // Check for division by zero BEFORE dividing
        {
            write(1, "Stop: division by zero\n", 22);  // Print error message
            return (0);  // Exit with error
        }
        result = a / b;  // Safe to divide
    }
    else if (argv[2][0] == '%')  // Modulo (remainder)
    {
        if (b == 0)  // Check for modulo by zero BEFORE computing
        {
            write(1, "Stop: modulo by zero\n", 20);  // Print error message
            return (0);  // Exit with error
        }
        result = a % b;  // Safe to compute remainder
    }
    else  // Unknown operator character
        return (0);  // Exit quietly for invalid operator
    ft_putnbr(result);  // Print the computed result
    write(1, "\n", 1);  // Print newline after result
    return (0);  // Success
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 21 | `#include <unistd.h>` | Header for write() system call |
| 26 | `int main(int argc, char **argv)` | Entry point: program name, then num1, op, num2 |
| 32 | `if (argc != 4)` | Must have exactly 4 arguments: ./program 5 + 3 |
| 33 | `return (0);` | Wrong arg count; silently exit |
| 35 | `a = ft_atoi(argv[1]);` | Convert first string argument to integer |
| 36 | `b = ft_atoi(argv[3]);` | Convert third string argument to integer |
| 38-40 | (addition) | If operator is '+', compute a + b |
| 42-44 | (subtraction) | If operator is '-', compute a - b |
| 46-48 | (multiplication) | If operator is '*', compute a * b |
| 50-57 | (division) | If operator is '/', check for zero divisor first |
| 59-66 | (modulo) | If operator is '%', check for zero divisor first |
| 68-69 | (invalid op) | Unknown operator; exit silently |
| 71 | `ft_putnbr(result);` | Print the computed answer |
| 72 | `write(1, "\n", 1);` | Add newline after output |

## Common Traps
- ❌ Not handling division/modulo by zero.
- ❌ Not checking argument count.
- ❌ Not printing newline after result.
- ❌ Using wrong operator check.
