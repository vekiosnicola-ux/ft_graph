---
tags: []
date: 2026-03-29
status: complete
---
# search_and_replace

EXAMS INDEX|Exam INDEX | Level 1

---
tags: [Exams, Level_1, magenta]
---

## What it does
Takes 3 arguments: a string, a character to find, and a character to replace. Replaces ALL occurrences of the find character with the replace character in the string, then prints the result followed by a newline.

## Insight
This is a direct application of the "Invisible Skeleton" with a conditional action inside the loop. The key insight is:
1. You iterate through each character of the string
2. If the current character matches the "find" character, you print the "replace" character instead
3. Otherwise, you print the original character
4. All three arguments are required (av[1], av[2], av[3]), and av[2]/av[3] must be single characters

## Step-by-step Algorithm
1. Check if exactly 3 arguments provided (ac == 4, since ac=1 is program name)
2. Also check that find and replace args are single chars (av[2][1] == '\0' and av[3][1] == '\0')
3. Initialize index i = 0
4. While str[i] (av[1][i]) is not '\0':
   - If av[1][i] equals av[2][0] (find char), write av[3][0] (replace char)
   - Else, write av[1][i] unchanged
   - Increment i
5. Write a newline

## Code
```c
 <unistd.h>       // Required for write() system call

void search_and_replace(char *str, char find, char replace)  // Takes string and two chars
{
    int i = 0;             // Index for traversing string
    
    while (str[i] != '\0')  // Loop through entire string (Invisible Skeleton)
    {
        if (str[i] == find)                    // If current char matches find character
            write(1, &replace, 1);               // Write the replace character instead
        else                                    // Otherwise
            write(1, &str[i], 1);               // Write the original character
        i++;                                     // Move to next character
    }
}

int main(int ac, char **av)  // Main receives argc and argv
{
    // Check: exactly 4 args AND av[2] is single char AND av[3] is single char
    if (ac == 4 && av[2][1] == '\0' && av[3][1] == '\0')
        search_and_replace(av[1], av[2][0], av[3][0]);  // Pass string, find char, replace char
    write(1, "\n", 1);      // Always print newline at end
    return (0);              // Exit with success
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|-------------|
| 1 | `#include <unistd.h>` | Include header for `write()` system call |
| 3 | `void search_and_replace(char *str, char find, char replace)` | Function: string + two chars |
| 4 | `{` | Start of function body |
| 5 | `int i = 0;` | Initialize index to 0 |
| 7 | `while (str[i] != '\0')` | Loop through entire string |
| 8 | `{` | Start of while body |
| 9 | `if (str[i] == find)` | Check if current char matches find character |
| 10 | `write(1, &replace, 1);` | Write replace character instead |
| 11 | `else` | Current char doesn't match find |
| 12 | `write(1, &str[i], 1);` | Write original character |
| 13 | `i++;` | Move to next character |
| 14 | `}` | End of while body |
| 15 | `}` | End of search_and_replace |
| 17 | `int main(int ac, char **av)` | Main with argc and argv |
| 18 | `{` | Start of main body |
| 19 | `if (ac == 4 && av[2][1] == '\0' && av[3][1] == '\0')` | Check 3 args + single chars |
| 20 | `search_and_replace(av[1], av[2][0], av[3][0]);` | Call with string, find, replace |
| 21 | `write(1, "\n", 1);` | Print newline |
| 22 | `return (0);` | Exit with success |
| 23 | `}` | End of main |

## Common Traps
- ❌ Forgetting to check ac == 4 (need exactly 3 args + program name)
- ❌ Not checking that find/replace are single chars (av[2][1] == '\0')
- ❌ Forgetting to write the newline at the end
- ❌ Using write(1, replace, 1) instead of write(1, &replace, 1) (segfault)
- ❌ Forgetting to increment i (infinite loop)
- ❌ Not handling the case where no replacement is needed (just print original)

## Propedeuticity
- [[ft_putstr]] - String iteration skeleton
- [[aff_first_param]] - Understanding av array access

## Related Exercises
- [[ulstr]] - Character transformation in strings
- [[rot_13]] - Similar string iteration with character mapping

(End of file - 91 lines)
