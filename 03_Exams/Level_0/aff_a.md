---
tags: []
date: 2026-03-29
status: complete
---
# aff_a

EXAMS INDEX|Exam INDEX | Level 0

---
tags: [Exams, Level_0, magenta]
---


## What it does
Finds and displays the first occurrence of the letter 'a' in a string passed as argument. If no 'a' is found, displays nothing.

## Insight
This introduces the "Invisible Skeleton" pattern with an early exit condition. The key insight is that you're searching for a specific character, not just counting or transforming.

When you find the target, you output it and return immediately - no need to look further.

## Step-by-step Algorithm
1. Check if an argument was provided (ac > 1)
2. If yes, get the string from av[1]
3. Initialize index i = 0
4. While str[i] is not '\0':
   - If str[i] == 'a', write it and return (we found it!)
   - Otherwise, increment i and continue
5. If loop ends without finding 'a', write nothing

## Code
```c
 <unistd.h>      // Required for write() system call

void aff_a(char *str)    // Function takes a string pointer
{
    int i = 0;           // Initialize index to 0 (start of string)
    
    while (str[i] != '\0')  // Loop until end of string (Invisible Skeleton)
    {
        if (str[i] == 'a')    // If current character is 'a'
        {
            write(1, &str[i], 1);  // Write just that character (1 byte)
            return;                // Exit function immediately after finding 'a'
        }
        i++;                   // Move to next character
    }
}

int main(int ac, char **av)  // Main receives argc and argv
{
    if (ac == 2)             // Check that exactly 2 args (program + string)
        aff_a(av[1]);         // Pass the first argument to aff_a
    write(1, "\n", 1);       // Always print newline at end
    return (0);               // Exit with success
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|-------------|
| 1 | `#include <unistd.h>` | Include header for `write()` system call |
| 3 | `void aff_a(char *str)` | Define function taking a string pointer, returns nothing |
| 4 | `{` | Start of function body |
| 5 | `int i = 0;` | Declare index variable and initialize to 0 |
| 7 | `while (str[i] != '\0')` | Loop while current char is not null terminator |
| 8 | `{` | Start of while loop body |
| 9 | `if (str[i] == 'a')` | Check if current character is 'a' |
| 10 | `{` | Start of if body |
| 11 | `write(1, &str[i], 1);` | Write the 'a' character to stdout (1 byte) |
| 12 | `return;` | Exit function immediately (found it!) |
| 13 | `}` | End of if body |
| 14 | `i++;` | Move index to next character |
| 15 | `}` | End of while loop body |
| 16 | `}` | End of aff_a function |
| 18 | `int main(int ac, char **av)` | Define main with argument count and argument vector |
| 19 | `{` | Start of main body |
| 20 | `if (ac == 2)` | Check if exactly 2 arguments (program name + string) |
| 21 | `aff_a(av[1]);` | Call aff_a with the first command-line argument |
| 22 | `write(1, "\n", 1);` | Print a newline |
| 23 | `return (0);` | Exit with success code 0 |
| 24 | `}` | End of main |

## Common Traps
- ❌ Forgetting to check ac == 2 (no argument case)
- ❌ Not returning after finding 'a' (would continue searching)
- ❌ Writing str[i] instead of &str[i] to write() (causes segfault)
- ❌ Forgetting the final newline in main()
- ❌ Using av[0] instead of av[1] (av[0] is the program name)

## Propedeuticity
- [[aff_first_param]] - Understanding av[1] for arguments
- [[ft_strlen]] - String iteration foundation

## Related Exercises
- [[aff_z]] - Identical but searching for 'z'
- [[only_a]] - Counting all 'a' instead of finding first

(End of file - 86 lines)
