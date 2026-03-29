---
tags: []
date: 2026-03-29
status: complete
---
# first_word

EXAMS INDEX|Exam INDEX | Level 1

---
tags: [Exams, Level_1, magenta]
---

## What it does
Displays the first word of a string passed as argument, followed by a newline. A word is a sequence of non-space/non-tab characters. Leading spaces/tabs are skipped.

## Insight
This teaches you how to skip unwanted characters and then capture a sequence of wanted characters. The key insight is a two-phase approach:
1. Phase 1: Skip leading spaces/tabs
2. Phase 2: Print characters until you hit a space/tab or end of string

This is the "skip-then-process" pattern.

## Step-by-step Algorithm
1. Check if an argument was provided (ac > 1)
2. If yes, get the string from av[1]
3. Initialize index i = 0
4. **Skip leading spaces/tabs**: while str[i] is space or tab, increment i
5. **Print the word**: while str[i] is not space/tab and not '\0':
   - Write str[i]
   - Increment i
6. Write a newline

## Code
```c
 <unistd.h>       // Required for write() system call

void first_word(char *str)  // Function takes a string pointer
{
    int i = 0;             // Index for traversing the string
    
    // Skip leading spaces and tabs
    while (str[i] == ' ' || str[i] == '\t')  // While current char is space OR tab
        i++;                                 // Move to next character
    
    // Print the first word (until space, tab, or end)
    while (str[i] != '\0' && str[i] != ' ' && str[i] != '\t')  // While not at end and not whitespace
    {
        write(1, &str[i], 1);   // Write current character
        i++;                     // Move to next character
    }
}

int main(int ac, char **av)  // Main receives argc and argv
{
    if (ac == 2)             // Check that exactly 2 args (program + string)
        first_word(av[1]);   // Pass the first argument to first_word
    write(1, "\n", 1);      // Always print newline at end
    return (0);              // Exit with success
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|-------------|
| 1 | `#include <unistd.h>` | Include header for `write()` system call |
| 3 | `void first_word(char *str)` | Define function taking a string pointer |
| 4 | `{` | Start of function body |
| 5 | `int i = 0;` | Initialize index to 0 |
| 7 | `while (str[i] == ' ' \|\| str[i] == '\t')` | Skip spaces and tabs |
| 8 | `i++;` | Move index forward |
| 10 | `while (str[i] != '\0' && str[i] != ' ' && str[i] != '\t')` | While not at end and not whitespace |
| 11 | `{` | Start of while body |
| 12 | `write(1, &str[i], 1);` | Write current character |
| 13 | `i++;` | Move to next character |
| 14 | `}` | End of while body |
| 15 | `}` | End of first_word |
| 17 | `int main(int ac, char **av)` | Main with argc and argv |
| 18 | `{` | Start of main body |
| 19 | `if (ac == 2)` | Check if exactly 2 arguments |
| 20 | `first_word(av[1]);` | Call first_word with first argument |
| 21 | `write(1, "\n", 1);` | Print newline |
| 22 | `return (0);` | Exit with success |
| 23 | `}` | End of main |

## Common Traps
- ❌ Forgetting to check ac == 2
- ❌ Forgetting to skip leading spaces/tabs
- ❌ Using wrong condition in second loop (e.g., only checking for space but not tab)
- ❌ Not incrementing i in either loop (infinite loop)
- ❌ Writing str[i] instead of &str[i] to write() (segfault)
- ❌ Forgetting the final newline
- ❌ Using av[0] instead of av[1]

## Propedeuticity
- [[ft_putstr]] - String iteration
- [[aff_first_param]] - Understanding av[1]

## Related Exercises
- [[rev_print]] - Reverse string traversal
- [[ft_putstr]] - Basic string output

(End of file - 90 lines)
