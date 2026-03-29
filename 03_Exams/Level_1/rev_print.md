---
tags: []
date: 2026-03-29
status: complete
---
# rev_print

EXAMS INDEX|Exam INDEX | Level 1

---
tags: [Exams, Level_1, magenta]
---

## What it does
Displays a string passed as argument in reverse order, followed by a newline.

## Insight
This teaches you how to traverse a string backwards. The key insight is:
1. First, find the end of the string (the null terminator)
2. Then, work backwards from the last character to the first
3. For each character, write it to stdout
4. Finally, write a newline

This requires a two-pass approach: find end first, then work backwards.

## Step-by-step Algorithm
1. Check if the string is not NULL
2. Initialize index i = 0
3. **Find the end**: while str[i] is not '\0', increment i (now i points to '\0')
4. **Work backwards**: while i > 0:
   - Decrement i (now points to last character)
   - Write str[i]
   - Continue until i == 0 (we've written the first character)
5. Write a newline

## Code
```c
 <unistd.h>       // Required for write() system call

void rev_print(char *str)  // Function takes a string pointer
{
    int i = 0;             // Index for finding end of string
    
    if (!str)              // Safety check: if string is NULL
        return;            // Exit function gracefully
    
    // Find the end of the string
    while (str[i] != '\0')  // Loop until we reach the null terminator
        i++;                 // i now points one past the last character
    
    // Work backwards from the last character
    while (i > 0)           // While there are characters left to print
    {
        i--;                 // Move to previous character (backwards!)
        write(1, &str[i], 1);  // Write that character
    }
}

int main(int ac, char **av)  // Main receives argc and argv
{
    if (ac == 2)             // Check that exactly 2 args (program + string)
        rev_print(av[1]);    // Pass the first argument to rev_print
    write(1, "\n", 1);      // Always print newline at end
    return (0);              // Exit with success
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|-------------|
| 1 | `#include <unistd.h>` | Include header for `write()` system call |
| 3 | `void rev_print(char *str)` | Define function taking a string pointer |
| 4 | `{` | Start of function body |
| 5 | `int i = 0;` | Initialize index to 0 |
| 7 | `if (!str)` | Check if string pointer is NULL |
| 8 | `return;` | Exit function early if NULL |
| 10 | `while (str[i] != '\0')` | Find end of string |
| 11 | `i++;` | Move forward until null terminator |
| 13 | `while (i > 0)` | Work backwards while characters remain |
| 14 | `{` | Start of while body |
| 15 | `i--;` | Move index backwards (to previous character) |
| 16 | `write(1, &str[i], 1);` | Write current character |
| 17 | `}` | End of while body |
| 18 | `}` | End of rev_print |
| 20 | `int main(int ac, char **av)` | Main with argc and argv |
| 21 | `{` | Start of main body |
| 22 | `if (ac == 2)` | Check exactly 2 arguments |
| 23 | `rev_print(av[1]);` | Call rev_print with first argument |
| 24 | `write(1, "\n", 1);` | Print newline |
| 25 | `return (0);` | Exit with success |
| 26 | `}` | End of main |

## Common Traps
- ❌ Forgetting to check for NULL string
- ❌ Forgetting to find the end first (trying to work backwards from i=0)
- ❌ Using wrong loop condition (e.g., while (i >= 0) which would access str[-1])
- ❌ Forgetting to decrement i before writing in the second loop
- ❌ Writing str[i] instead of &str[i] to write() (segfault)
- ❌ Forgetting the final newline
- ❌ Using av[0] instead of av[1]

## Propedeuticity
- [[ft_putstr]] - String iteration
- [[ft_strlen]] - Finding string length

## Related Exercises
- [[first_word]] - String parsing in forward direction
- [[ft_strlen]] - String length calculation

(End of file - 97 lines)
