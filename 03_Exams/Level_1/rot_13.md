---
tags: []
date: 2026-03-29
status: complete
---
# rot_13

EXAMS INDEX|Exam INDEX | Level 1

---
tags: [Exams, Level_1, magenta]
---

## What it does
Applies the ROT13 cipher to a string passed as argument and prints the result, followed by a newline. ROT13 shifts each letter by 13 positions in the alphabet (wrapping around), preserving case. Non-alphabetic characters are unchanged.

## Insight
This teaches you character transformation with wrapping. The key insight is:
1. For each character, check if it's a letter
2. If uppercase (A-Z): shift by 13, wrapping from Z to A
3. If lowercase (a-z): shift by 13, wrapping from z to a
4. Non-letters are printed unchanged
5. This can be done by checking ranges and applying modular arithmetic, or by checking if the shifted char goes past 'Z' or 'z'

## Step-by-step Algorithm
1. Check if an argument was provided (ac > 1)
2. If yes, get the string from av[1]
3. Initialize index i = 0
4. While str[i] is not '\0':
   - If str[i] is between 'A' and 'Z':
     - Add 13 to str[i]
     - If result > 'Z', subtract 26 to wrap around
     - Write the result
   - Else if str[i] is between 'a' and 'z':
     - Add 13 to str[i]
     - If result > 'z', subtract 26 to wrap around
     - Write the result
   - Else: write str[i] unchanged
   - Increment i
5. Write a newline

## Code
```c
 <unistd.h>       // Required for write() system call

void rot_13(char *str)    // Function takes a string pointer
{
    int i = 0;             // Index for traversing string
    
    while (str[i] != '\0')  // Loop while not at end of string
    {
        if (str[i] >= 'A' && str[i] <= 'Z')  // Check if uppercase letter
        {
            str[i] += 13;                       // Shift by 13 forward
            if (str[i] > 'Z')                   // If past 'Z', wrap around
                str[i] -= 26;                     // Subtract 26 (full alphabet)
            write(1, &str[i], 1);               // Write transformed char
        }
        else if (str[i] >= 'a' && str[i] <= 'z')  // Check if lowercase letter
        {
            str[i] += 13;                         // Shift by 13 forward
            if (str[i] > 'z')                     // If past 'z', wrap around
                str[i] -= 26;                       // Subtract 26 (full alphabet)
            write(1, &str[i], 1);                 // Write transformed char
        }
        else
            write(1, &str[i], 1);               // Non-letters: write unchanged
        i++;                                     // Move to next character
    }
}

int main(int ac, char **av)  // Main receives argc and argv
{
    if (ac == 2)             // Check that exactly 2 args (program + string)
        rot_13(av[1]);       // Pass the first argument to rot_13
    write(1, "\n", 1);      // Always print newline at end
    return (0);              // Exit with success
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|-------------|
| 1 | `#include <unistd.h>` | Include header for `write()` system call |
| 3 | `void rot_13(char *str)` | Define function taking a string pointer |
| 4 | `{` | Start of function body |
| 5 | `int i = 0;` | Initialize index to 0 |
| 7 | `while (str[i] != '\0')` | Loop through entire string |
| 8 | `{` | Start of while body |
| 9 | `if (str[i] >= 'A' && str[i] <= 'Z')` | Check if uppercase letter |
| 10 | `{` | Start of uppercase block |
| 11 | `str[i] += 13;` | Add 13 to shift forward |
| 12 | `if (str[i] > 'Z')` | Check if wrapped past 'Z' |
| 13 | `str[i] -= 26;` | Wrap around by subtracting full alphabet |
| 14 | `write(1, &str[i], 1);` | Write the shifted character |
| 15 | `}` | End of uppercase block |
| 16 | `else if (str[i] >= 'a' && str[i] <= 'z')` | Check if lowercase letter |
| 17 | `{` | Start of lowercase block |
| 18 | `str[i] += 13;` | Add 13 to shift forward |
| 19 | `if (str[i] > 'z')` | Check if wrapped past 'z' |
| 20 | `str[i] -= 26;` | Wrap around by subtracting full alphabet |
| 21 | `write(1, &str[i], 1);` | Write the shifted character |
| 22 | `}` | End of lowercase block |
| 23 | `else` | Non-alphabetic character |
| 24 | `write(1, &str[i], 1);` | Write unchanged |
| 25 | `i++;` | Move to next character |
| 26 | `}` | End of while body |
| 27 | `}` | End of rot_13 |
| 29 | `int main(int ac, char **av)` | Main with argc and argv |
| 30 | `{` | Start of main body |
| 31 | `if (ac == 2)` | Check exactly 2 arguments |
| 32 | `rot_13(av[1]);` | Call rot_13 with first argument |
| 33 | `write(1, "\n", 1);` | Print newline |
| 34 | `return (0);` | Exit with success |
| 35 | `}` | End of main |

## Common Traps
- ❌ Forgetting to check both uppercase and lowercase ranges
- ❌ Forgetting to wrap around (e.g., just adding 13 without checking if > 'Z' or > 'z')
- ❌ Using wrong wrap amount (should be 26, not 13)
- ❌ Not incrementing i (infinite loop)
- ❌ Writing str[i] instead of &str[i] to write() (segfault)
- ❌ Forgetting the final newline
- ❌ Using av[0] instead of av[1]
- ❌ Modifying the original string (this exercise allows it, but be aware)

## Propedeuticity
- [[ft_putstr]] - String iteration
- [[ulstr]] - Character transformation basics

## Related Exercises
- [[rotone]] - Shift by 1 instead of 13
- [[ulstr]] - Case transformation without shifting

(End of file - 124 lines)
