---
tags: []
date: 2026-03-29
status: complete
---
# aff_last_param

EXAMS INDEX|Exam INDEX | Level 0

---
tags: [Exams, Level_0, magenta]
---


## What it does
Displays the last command-line argument followed by a newline. If no arguments are provided, displays nothing.

## Insight
Similar to aff_first_param, but you need to find the LAST argument. The key insight is that av[ac-1] is the last argument (since av[ac] is NULL, av[0] is the program name).

This exercise teaches you that argv is an array where the last valid index is ac-1.

## Step-by-step Algorithm
1. Check if ac > 1 (at least one argument provided)
2. If yes, the last argument is at av[ac-1]
3. Use ft_putstr to print that string
4. Write a newline after
5. If no arguments, just write newline or nothing

## Code
```c
 <unistd.h>       // Required for write() system call

void ft_putstr(char *str)  // Helper function to print a string
{
    int i = 0;             // Index starts at 0
    
    while (str[i] != '\0')  // Loop until end of string (Invisible Skeleton)
    {
        write(1, &str[i], 1);  // Write one character at a time
        i++;                   // Move to next character
    }
}

int main(int ac, char **av)  // Main: ac=count, av=array of argument strings
{
    if (ac >= 2)             // If at least 2 args (program name + one param)
        ft_putstr(av[ac - 1]);  // Print LAST argument: av[ac-1], NOT av[ac]!
    write(1, "\n", 1);       // Always print newline at the end
    return (0);               // Exit with success code 0
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|-------------|
| 1 | `#include <unistd.h>` | Include header for `write()` system call |
| 3 | `void ft_putstr(char *str)` | Define function that prints a string |
| 4 | `{` | Start of function body |
| 5 | `int i = 0;` | Declare and initialize index to 0 |
| 7 | `while (str[i] != '\0')` | Loop while not at null terminator |
| 8 | `{` | Start of while body |
| 9 | `write(1, &str[i], 1);` | Write current character to stdout |
| 10 | `i++;` | Move index to next character |
| 11 | `}` | End of while body |
| 12 | `}` | End of ft_putstr function |
| 14 | `int main(int ac, char **av)` | Main with argument count and vector |
| 15 | `{` | Start of main body |
| 16 | `if (ac >= 2)` | Check that at least 2 arguments exist |
| 17 | `ft_putstr(av[ac - 1]);` | Print the LAST argument (av[ac-1]) |
| 18 | `write(1, "\n", 1);` | Print a newline |
| 19 | `return (0);` | Exit with success code 0 |
| 20 | `}` | End of main |

## Common Traps
- ❌ Using av[ac] instead of av[ac-1] (av[ac] is NULL)
- ❌ Forgetting the ac >= 2 check
- ❌ Not writing the newline
- ❌ Confusing av (array of strings) with ac (argument count)
- ❌ Trying to loop through all args when you just need the last one

## Propedeuticity
- [[aff_first_param]] - Understanding argument access
- [[ft_putstr]] - String output

## Related Exercises
- [[aff_first_param]] - Access first argument instead of last
- [[hello]] - Basic write output

(End of file - 76 lines)
