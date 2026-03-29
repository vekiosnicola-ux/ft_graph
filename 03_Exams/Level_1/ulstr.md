---
tags: []
date: 2026-03-29
status: complete
---
# ulstr

EXAMS INDEX|Exam INDEX | Level 1

---
tags: [Exams, Level_1, magenta]
---

## What it does
Toggles the case of each letter in the string passed as argument: uppercase becomes lowercase, lowercase becomes uppercase. Non-alphabetic characters are unchanged. The result is printed followed by a newline.

## Insight
This teaches you how to toggle case using ASCII properties. The key insight is:
1. For each character, check if it's a letter
2. If uppercase (A-Z): add 32 to make it lowercase
3. If lowercase (a-z): subtract 32 to make it uppercase
4. Non-letters are printed unchanged

The ASCII difference between uppercase and lowercase letters is exactly 32.

## Step-by-step Algorithm
1. Check if an argument was provided (ac > 1)
2. If yes, get the string from av[1]
3. Initialize index i = 0
4. While str[i] is not '\0':
   - If str[i] is between 'A' and 'Z':
     - Add 32 to make it lowercase
     - Write the result
   - Else if str[i] is between 'a' and 'z':
     - Subtract 32 to make it uppercase
     - Write the result
   - Else: write str[i] unchanged
   - Increment i
5. Write a newline

## Code
```c
 <unistd.h>       // Required for write() system call

void ulstr(char *str)     // Function takes a string pointer
{
    int i = 0;             // Index for traversing string
    
    while (str[i] != '\0')  // Loop while not at end of string
    {
        if (str[i] >= 'A' && str[i] <= 'Z')  // If uppercase letter
            write(1, &(str[i] + 32), 1);        // Add 32: 'A'->'a', 'B'->'b', etc.
        else if (str[i] >= 'a' && str[i] <= 'z')  // If lowercase letter
            write(1, &(str[i] - 32), 1);            // Subtract 32: 'a'->'A', 'b'->'B', etc.
        else                                    // Non-letter
            write(1, &str[i], 1);               // Write unchanged
        i++;                                     // Move to next character
    }
}

int main(int ac, char **av)  // Main receives argc and argv
{
    if (ac == 2)             // Check that exactly 2 args (program + string)
        ulstr(av[1]);       // Pass the first argument to ulstr
    write(1, "\n", 1);      // Always print newline at end
    return (0);              // Exit with success
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|-------------|
| 1 | `#include <unistd.h>` | Include header for `write()` system call |
| 3 | `void ulstr(char *str)` | Define function taking a string pointer |
| 4 | `{` | Start of function body |
| 5 | `int i = 0;` | Initialize index to 0 |
| 7 | `while (str[i] != '\0')` | Loop through entire string |
| 8 | `{` | Start of while body |
| 9 | `if (str[i] >= 'A' && str[i] <= 'Z')` | Check if uppercase letter |
| 10 | `write(1, &(str[i] + 32), 1);` | Transform to lowercase by adding 32 (ASCII diff) |
| 11 | `else if (str[i] >= 'a' && str[i] <= 'z')` | Check if lowercase letter |
| 12 | `write(1, &(str[i] - 32), 1);` | Transform to uppercase by subtracting 32 |
| 13 | `else` | Non-alphabetic character |
| 14 | `write(1, &str[i], 1);` | Write unchanged |
| 15 | `i++;` | Move to next character |
| 16 | `}` | End of while body |
| 17 | `}` | End of ulstr |
| 19 | `int main(int ac, char **av)` | Main with argc and argv |
| 20 | `{` | Start of main body |
| 21 | `if (ac == 2)` | Check exactly 2 arguments |
| 22 | `ulstr(av[1]);` | Call ulstr with first argument |
| 23 | `write(1, "\n", 1);` | Print newline |
| 24 | `return (0);` | Exit with success |
| 25 | `}` | End of main |

## Common Traps
- ❌ Forgetting to check both uppercase and lowercase ranges
- ❌ Using wrong offset (should be 32, not other values)
- ❌ Forgetting to preserve non-alphabetic characters
- ❌ Not incrementing i (infinite loop)
- ❌ Writing str[i] instead of &str[i] to write() (segfault)
- ❌ Forgetting the final newline
- ❌ Using av[0] instead of av[1]

## Propedeuticity
- [[ft_putstr]] - String iteration
- [[maff_alpha]] - Understanding ASCII case conversion (32 offset)

## Related Exercises
- [[rot_13]] - Character transformation
- [[rotone]] - Rotating characters by 1
- [[search_and_replace]] - Character replacement

(End of file - 101 lines)
