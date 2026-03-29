---
tags: [Level_2, exam]
  - calculator
Level: 2
Topic: Algorithms
Exercise: do_op
---


# do_op

## What It Does
Calculator taking "value1 operator value2" as command-line arguments and prints the result. Supports operators: `+ - * / %`

## The Insight
Use ft_atoi to parse operands, switch statement for operator. Must handle division and modulo by zero (don't crash, just skip computation).

## Step-by-Step Algorithm
1. Parse `av[1]` and `av[3]` with ft_atoi
2. Use switch on `av[2][0]` (the operator character)
3. Perform the arithmetic operation
4. Print result with ft_putnbr

## Code
```c
int a = ft_atoi(av[1]);                          // Convert first operand from string to int
int b = ft_atoi(av[3]);                          // Convert second operand from string to int
int r;                                            // Result variable to store computed value

switch (av[2][0])                                 // Switch on the operator character (first char of arg 2)
{
    case '+':                                     // Addition operator
        r = a + b;                                // Compute sum of a and b
        break;                                    // Exit switch statement
    case '-':                                     // Subtraction operator
        r = a - b;                                // Compute difference of a and b
        break;                                    // Exit switch statement
    case '*':                                     // Multiplication operator
        r = a * b;                                // Compute product of a and b
        break;                                    // Exit switch statement
    case '/':                                     // Division operator
        if (b != 0)                               // Check for division by zero
            r = a / b;                            // Compute quotient if divisor is safe
        break;                                    // Exit switch statement
    case '%':                                     // Modulo operator
        if (b != 0)                               // Check for modulo by zero
            r = a % b;                            // Compute remainder if divisor is safe
        break;                                    // Exit switch statement
}
ft_putnbr(r);                                     // Print the computed result as number
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int a = ft_atoi(av[1]);` | Parse first number from argument 1 |
| `int b = ft_atoi(av[3]);` | Parse second number from argument 3 |
| `int r;` | Declare result variable |
| `switch (av[2][0])` | Switch on operator character (argument 2, first char) |
| `case '+':` | Addition case |
| `r = a + b;` | Compute sum |
| `break;` | Break out of switch |
| `case '-':` | Subtraction case |
| `r = a - b;` | Compute difference |
| `break;` | Break out of switch |
| `case '*':` | Multiplication case |
| `r = a * b;` | Compute product |
| `break;` | Break out of switch |
| `case '/':` | Division case |
| `if (b != 0)` | Check divisor is not zero |
| `r = a / b;` | Compute quotient |
| `break;` | Break out of switch |
| `case '%':` | Modulo case |
| `if (b != 0)` | Check divisor is not zero |
| `r = a % b;` | Compute remainder |
| `break;` | Break out of switch |
| `ft_putnbr(r);` | Print the computed result |

## Common Traps
- ❌ Division/modulo by zero (causes crash if not checked)
- ❌ Not handling negative numbers in ft_atoi
- ❌ Wrong operand order in division (a / b vs b / a)
- ❌ Missing break statements (fall-through behavior)
- ❌ Not including ft_atoi and ft_putnbr prototypes

## Related Exercises
- [[ft_atoi]] - Number string parsing
- [[ft_putnbr]] - Number printing
- [[tab_mult]] - Multiplication table with formatting

## Wiki Links
03_Exams/Level_2_INDEX|Level 2 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 93 lines)
