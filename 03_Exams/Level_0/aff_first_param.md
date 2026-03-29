---
tags: []
date: 2026-03-29
status: complete
---
# aff_first_param

EXAMS INDEX|Exam INDEX | Level 0

---
tags: [Exams, Level_0, magenta]
---


## What it does
Displays the first command-line argument followed by a newline. If no arguments are provided, displays nothing.

## Insight
This teaches you how to access command-line arguments in C. The key insight is understanding the argv array:
- av[0] is the program name
- av[1] is the first argument
- av[ac-1] is the last argument
- av[ac] is NULL

This is the foundation for all argument-based exercises.

## Step-by-step Algorithm
1. Check if ac > 1 (at least one argument provided)
2. If yes, av[1] points to the first argument string
3. Use ft_putstr (or equivalent) to print the entire string
4. Write a newline after
5. If no arguments, just write the newline

## Code
```c
 <unistd.h>       // Required for write() system call

void ft_putstr(char *str)  // Function to print a string
{
    int i = 0;             // Index variable, starts at 0
    
    while (str[i] != '\0')  // Loop while not at end of string (Invisible Skeleton)
    {
        write(1, &str[i], 1);  // Write one character at a time
        i++;                   // Move to next character
    }
}

int main(int ac, char **av)  // Main receives argument count and vector
{
    if (ac >= 2)             // If at least 2 args (program name + one param)
        ft_putstr(av[1]);    // Print the first argument (av[1])
    write(1, "\n", 1);      // Always print a newline at the end
    return (0);             // Exit with success
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|-------------|
| 1 | `#include <unistd.h>` | Include header for `write()` system call |
| 3 | `void ft_putstr(char *str)` | Define function taking a string, returns nothing |
| 4 | `{` | Start of function body |
| 5 | `int i = 0;` | Declare and initialize index to 0 |
| 7 | `while (str[i] != '\0')` | Loop until null terminator is reached |
| 8 | `{` | Start of while body |
| 9 | `write(1, &str[i], 1);` | Write current character to stdout (1 byte) |
| 10 | `i++;` | Increment index to move to next character |
| 11 | `}` | End of while body |
| 12 | `}` | End of ft_putstr function |
| 14 | `int main(int ac, char **av)` | Main: argc count, argv array of strings |
| 15 | `{` | Start of main body |
| 16 | `if (ac >= 2)` | Check if at least 2 arguments exist |
| 17 | `ft_putstr(av[1]);` | Print the first argument (av[1], not av[0]) |
| 18 | `write(1, "\n", 1);` | Print a newline |
| 19 | `return (0);` | Exit program with success code |
| 20 | `}` | End of main |

## Common Traps
- ❌ Using av[0] instead of av[1] (prints program name)
- ❌ Forgetting to check ac >= 2 (will segfault if no arguments)
- ❌ Not writing the newline after the argument
- ❌ Trying to modify av[1] (it's read-only)
- ❌ Using printf instead of write/ft_putstr

## Propedeuticity
- [[hello]] - Basic write output
- [[ft_putstr]] - String iteration

## Related Exercises
- [[aff_last_param]] - Access last argument instead of first
- [[only_a]] - Similar string iteration with av[1]

(End of file - 76 lines)
