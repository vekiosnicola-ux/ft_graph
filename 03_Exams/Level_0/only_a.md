---
tags: []
date: 2026-03-29
status: complete
---
# only_a

EXAMS INDEX|Exam INDEX | Level 0

---
tags: [Exams, Level_0, magenta]
---


## What it does
Counts the number of 'a' characters in a string passed as argument and prints that count followed by a newline.

## Insight
This introduces counting with a condition. The key insight is:
1. Iterate through the entire string
2. For each character, if it's 'a', increment a counter
3. After the loop, print the counter value

This follows the "Invisible Skeleton" pattern with a conditional increment inside the loop.

## Step-by-step Algorithm
1. Check if an argument was provided (ac > 1)
2. If yes, get the string from av[1]
3. Initialize counter = 0 and index i = 0
4. While str[i] is not '\0':
   - If str[i] == 'a', increment counter
   - Increment i
5. After loop, print the counter value (using ft_putnbr)
6. Write a newline

## Code
```c
 <unistd.h>       // Required for write() system call

void ft_putnbr(int nb)    // Recursive function to print an integer
{
    if (nb < 0)           // If number is negative
    {
        write(1, "-", 1);  // Write minus sign
        nb = -nb;           // Make number positive for processing
    }
    if (nb >= 10)         // If number has multiple digits
        ft_putnbr(nb / 10);  // Recursively print all digits except last
    write(1, &"0123456789"[nb % 10], 1);  // Write last digit using lookup table
}

int main(int ac, char **av)  // Main receives argument count and vector
{
    int i = 0;               // Index for iterating through string
    int count = 0;           // Counter for 'a' characters found
    
    if (ac == 2)             // If exactly 2 args (program name + string)
    {
        while (av[1][i] != '\0')  // Loop through the entire argument string
        {
            if (av[1][i] == 'a')  // If current character is 'a'
                count++;            // Increment the counter
            i++;                   // Move to next character
        }
        ft_putnbr(count);      // Print the total count
    }
    write(1, "\n", 1);       // Always print a newline at the end
    return (0);               // Exit with success code 0
}
```

## Line-by-Line Translation
| Line | Code                                   | Translation                                |
| ---- | -------------------------------------- | ------------------------------------------ |
| 1    | `#include <unistd.h>`                  | Include header for `write()` system call   |
| 3    | `void ft_putnbr(int nb)`               | Define recursive function to print integer |
| 4    | `{`                                    | Start of ft_putnbr body                    |
| 5    | `if (nb < 0)`                          | Check if number is negative                |
| 6    | `{`                                    | Start of negative handling block           |
| 7    | `write(1, "-", 1);`                    | Write minus sign                           |
| 8    | `nb = -nb;`                            | Convert to positive                        |
| 9    | `}`                                    | End of negative handling block             |
| 10   | `if (nb >= 10)`                        | Check if multiple digits                   |
| 11   | `ft_putnbr(nb / 10);`                  | Recurse with all digits except last        |
| 12   | `write(1, &"0123456789"[nb % 10], 1);` | Write last digit                           |
| 13   | `}`                                    | End of ft_putnbr                           |
| 15   | `int main(int ac, char **av)`          | Main with argc and argv                    |
| 16   | `{`                                    | Start of main body                         |
| 17   | `int i = 0;`                           | Initialize string index to 0               |
| 18   | `int count = 0;`                       | Initialize 'a' counter to 0                |
| 20   | `if (ac == 2)`                         | Check exactly 2 arguments                  |
| 21   | `{`                                    | Start of if body                           |
| 22   | `while (av[1][i] != '\0')`             | Loop through entire argument string        |
| 23   | `{`                                    | Start of while body                        |
| 24   | `if (av[1][i] == 'a')`                 | Check if current char is 'a'               |
| 25   | `count++;`                             | Increment 'a' counter                      |
| 26   | `i++;`                                 | Move to next character                     |
| 27   | `}`                                    | End of while body                          |
| 28   | `ft_putnbr(count);`                    | Print the final count                      |
| 29   | `}`                                    | End of if body                             |
| 30   | `write(1, "\n", 1);`                   | Print newline                              |
| 31   | `return (0);`                          | Exit with success                          |
| 32   | `}`                                    | End of main                                |

## Common Traps
- ❌ Forgetting to check ac == 2
- ❌ Not resetting counter to 0
- ❌ Forgetting to increment i (infinite loop)
- ❌ Printing each 'a' instead of counting them
- ❌ Not writing the final newline
- ❌ Using av[0] instead of av[1]
- ❌ Forgetting to print the count (just counting internally)

## Propedeuticity
- [[hello]] - Basic output with write
- [[aff_first_param]] - Understanding av[1] for arguments
- [[ft_strlen]] - String iteration skeleton

## Related Exercises
- [[only_z]] - Identical but counting 'z'
- [[ft_strlen]] - String iteration foundation

(End of file - 104 lines)
