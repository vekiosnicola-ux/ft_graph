---
tags: []
date: 2026-03-29
status: complete
---
# aff_z

EXAMS INDEX|Exam INDEX | Level 0

---
tags: [Exams, Level_0, magenta]
---


## What it does
Finds and displays the first occurrence of the letter 'z' in a string passed as argument. If no 'z' is found, displays nothing.

## Insight
This is identical to aff_a but searching for 'z' instead of 'a'. It reinforces the search pattern and character comparison. The key insight is that you're searching for a specific character and stopping immediately when found.

This follows the "Invisible Skeleton" pattern with an early return when the target is found.

## Step-by-step Algorithm
1. Check if an argument was provided (ac > 1)
2. If yes, get the string from av[1]
3. Initialize index i = 0
4. While str[i] is not '\0':
   - If str[i] == 'z', write it and return (we found it!)
   - Otherwise, increment i and continue
5. If loop ends without finding 'z', write nothing

## Code
```c
 <unistd.h>      // Required for write() system call

void aff_z(char *str)    // Function takes a string pointer
{
    int i = 0;           // Initialize index to 0 (start of string)
    
    while (str[i] != '\0')  // Loop until end of string (Invisible Skeleton)
    {
        if (str[i] == 'z')    // If current character is 'z'
        {
            write(1, &str[i], 1);  // Write just that character (1 byte)
            return;                 // Exit function immediately after finding 'z'
        }
        i++;                   // Move to next character
    }
}

int main(int ac, char **av)  // Main receives argc and argv
{
    if (ac == 2)             // Check that exactly 2 args (program + string)
        aff_z(av[1]);         // Pass the first argument to aff_z
    write(1, "\n", 1);       // Always print newline at end
    return (0);               // Exit with success
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|-------------|
| 1 | `#include <unistd.h>` | Include header for `write()` system call |
| 3 | `void aff_z(char *str)` | Define function taking a string pointer, returns nothing |
| 4 | `{` | Start of function body |
| 5 | `int i = 0;` | Declare index variable and initialize to 0 |
| 7 | `while (str[i] != '\0')` | Loop while current char is not null terminator |
| 8 | `{` | Start of while loop body |
| 9 | `if (str[i] == 'z')` | Check if current character is 'z' |
| 10 | `{` | Start of if body |
| 11 | `write(1, &str[i], 1);` | Write the 'z' character to stdout (1 byte) |
| 12 | `return;` | Exit function immediately (found it!) |
| 13 | `}` | End of if body |
| 14 | `i++;` | Move index to next character |
| 15 | `}` | End of while loop body |
| 16 | `}` | End of aff_z function |
| 18 | `int main(int ac, char **av)` | Define main with argument count and argument vector |
| 19 | `{` | Start of main body |
| 20 | `if (ac == 2)` | Check if exactly 2 arguments (program name + string) |
| 21 | `aff_z(av[1]);` | Call aff_z with the first command-line argument |
| 22 | `write(1, "\n", 1);` | Print a newline |
| 23 | `return (0);` | Exit with success code 0 |
| 24 | `}` | End of main |

## Common Traps
- ❌ Forgetting to check ac == 2 (no argument case)
- ❌ Not returning after finding 'z' (would continue searching)
- ❌ Writing str[i] instead of &str[i] to write() (causes segfault)
- ❌ Forgetting the final newline in main()
- ❌ Using av[0] instead of av[1] (av[0] is the program name)

## Propedeuticity
- [[aff_a]] - Identical pattern for 'a'
- [[aff_first_param]] - Understanding av[1] for arguments

## Related Exercises
- [[aff_a]] - Identical but searching for 'a'

(End of file - 85 lines)
