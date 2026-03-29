---
tags: []
date: 2026-03-29
status: complete
---
# repeat_alpha

EXAMS INDEX|Exam INDEX | Level 1

---
tags: [Exams, Level_1, magenta]
---

## What it does
For each letter in the string passed as argument, prints the letter repeated as many times as its position in the alphabet (a=1, b=2, ..., z=26). Non-alphabetic characters are printed once. The result is followed by a newline.

## Insight
This teaches you how to map characters to repetition counts based on their alphabet position. The key insight is:
1. For each character, check if it's a letter
2. If uppercase (A-Z): position = (c - 'A' + 1)
3. If lowercase (a-z): position = (c - 'a' + 1)
4. Print the character that many times using a nested loop
5. Non-letters are printed once

This introduces nested loops: an outer loop for the string, an inner loop for repetitions.

## Step-by-step Algorithm
1. Check if an argument was provided (ac > 1)
2. If yes, get the string from av[1]
3. Initialize index i = 0
4. While str[i] is not '\0':
   - If str[i] is between 'A' and 'Z':
     - pos = str[i] - 'A' + 1
     - Write str[i] pos times
   - Else if str[i] is between 'a' and 'z':
     - pos = str[i] - 'a' + 1
     - Write str[i] pos times
   - Else: write str[i] once
   - Increment i
5. Write a newline

## Code
```c
 <unistd.h>       // Required for write() system call

void repeat_alpha(char *str)  // Function takes a string pointer
{
    int i = 0;             // Outer index for traversing string
    int j;                 // Inner counter for repetitions
    
    while (str[i] != '\0')  // Loop through each character
    {
        if (str[i] >= 'A' && str[i] <= 'Z')  // If uppercase letter
        {
            j = 0;                               // Initialize inner counter to 0
            while (j < (str[i] - 'A' + 1))       // Repeat (letter position) times
            {
                write(1, &str[i], 1);               // Write the letter once
                j++;                                 // Increment repetition counter
            }
        }
        else if (str[i] >= 'a' && str[i] <= 'z')  // If lowercase letter
        {
            j = 0;                               // Initialize inner counter to 0
            while (j < (str[i] - 'a' + 1))       // Repeat (letter position) times
            {
                write(1, &str[i], 1);               // Write the letter once
                j++;                                 // Increment repetition counter
            }
        }
        else                                    // Non-alphabetic character
            write(1, &str[i], 1);               // Write it once
        i++;                                     // Move to next character in string
    }
}

int main(int ac, char **av)  // Main receives argc and argv
{
    if (ac == 2)             // Check that exactly 2 args (program + string)
        repeat_alpha(av[1]);  // Pass the first argument to repeat_alpha
    write(1, "\n", 1);      // Always print newline at end
    return (0);              // Exit with success
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|-------------|
| 1 | `#include <unistd.h>` | Include header for `write()` system call |
| 3 | `void repeat_alpha(char *str)` | Define function taking a string pointer |
| 4 | `{` | Start of function body |
| 5 | `int i = 0;` | Outer index for string traversal |
| 6 | `int j;` | Inner counter for repetitions |
| 8 | `while (str[i] != '\0')` | Loop through each character in string |
| 9 | `{` | Start of outer while body |
| 10 | `if (str[i] >= 'A' && str[i] <= 'Z')` | Check if uppercase |
| 11 | `{` | Start of uppercase block |
| 12 | `j = 0;` | Reset inner counter |
| 13 | `while (j < (str[i] - 'A' + 1))` | Loop for repetitions (A=1, B=2, ...) |
| 14 | `{` | Start of inner while body |
| 15 | `write(1, &str[i], 1);` | Write the uppercase letter |
| 16 | `j++;` | Increment repetition counter |
| 17 | `}` | End of inner while body |
| 18 | `}` | End of uppercase block |
| 19 | `else if (str[i] >= 'a' && str[i] <= 'z')` | Check if lowercase |
| 20 | `{` | Start of lowercase block |
| 21 | `j = 0;` | Reset inner counter |
| 22 | `while (j < (str[i] - 'a' + 1))` | Loop for repetitions (a=1, b=2, ...) |
| 23 | `{` | Start of inner while body |
| 24 | `write(1, &str[i], 1);` | Write the lowercase letter |
| 25 | `j++;` | Increment repetition counter |
| 26 | `}` | End of inner while body |
| 27 | `}` | End of lowercase block |
| 28 | `else` | Non-alphabetic character |
| 29 | `write(1, &str[i], 1);` | Write it once |
| 30 | `i++;` | Move to next character in string |
| 31 | `}` | End of outer while body |
| 32 | `}` | End of repeat_alpha |
| 34 | `int main(int ac, char **av)` | Main with argc and argv |
| 35 | `{` | Start of main body |
| 36 | `if (ac == 2)` | Check exactly 2 arguments |
| 37 | `repeat_alpha(av[1]);` | Call repeat_alpha with first argument |
| 38 | `write(1, "\n", 1);` | Print newline |
| 39 | `return (0);` | Exit with success |
| 40 | `}` | End of main |

## Common Traps
- ❌ Forgetting to check both uppercase and lowercase ranges
- ❌ Using wrong position calculation (should be +1 for a=1, b=2, etc.)
- ❌ Not resetting the inner loop counter j for each character
- ❌ Not incrementing i (infinite loop)
- ❌ Writing str[i] instead of &str[i] to write() (segfault)
- ❌ Forgetting the final newline
- ❌ Using av[0] instead of av[1]

## Propedeuticity
- [[ft_putstr]] - String iteration
- [[ft_print_numbers]] - Nested loop understanding

## Related Exercises
- [[rot_13]] - Character transformation
- [[ulstr]] - Character case manipulation

(End of file - 131 lines)
