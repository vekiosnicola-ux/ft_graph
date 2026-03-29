---
tags: [Level_3, exam]
  - formatting
  - white
Level: 3
Topic: Algorithms
Exercise: tab_mult
---


# tab_mult

## What It Does
Prints multiplication table from 1 to 9 for a given number. Format: `"i x n = result"` followed by newline.

## The Insight
Loop 1 to 9. For each `i`, calculate `i*n`, print formatted string with `putnbr` for numbers.

## Step-by-Step Algorithm
1. `n = atoi(av[1])` — parse the number
2. Loop `i` from 1 to 9
3. For each: print `i`, `" x "`, `n`, `" = "`, `i*n`, `"\n"`

## Code
```c
int main(int ac, char **av)                      // Main: argument count and argument vector
{
    int n = atoi(av[1]);                        // Convert first argument string to integer
    int i = 1;                                  // Start multiplier at 1

    while (i <= 9)                              // Loop from 1 to 9 inclusive
    {
        putnbr(i);                               // Print the multiplier (1 through 9)
        write(1, " x ", 3);                     // Print " x " separator (exactly 3 bytes)
        putnbr(n);                               // Print the base number
        write(1, " = ", 3);                     // Print " = " separator (exactly 3 bytes)
        putnbr(i * n);                          // Print the product (i multiplied by n)
        write(1, "\n", 1);                      // Print newline after each line
        i++;                                     // Increment multiplier by 1
    }
}
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int main(int ac, char **av)` | Main function with argument count and argument vector |
| `{` | Start of main body |
| `int n = atoi(av[1]);` | Parse the number from first argument (av[1]) |
| `int i = 1;` | Initialize multiplier to 1 |
| `while (i <= 9)` | Loop while multiplier is 1 through 9 |
| `{` | Start of while body |
| `putnbr(i);` | Print the multiplier value |
| `write(1, " x ", 3);` | Print multiplication sign (3 bytes exactly) |
| `putnbr(n);` | Print the base number |
| `write(1, " = ", 3);` | Print equals sign (3 bytes exactly) |
| `putnbr(i * n);` | Print the product (multiplier times base) |
| `write(1, "\n", 1);` | Print newline after each line |
| `i++;` | Increment multiplier |
| `}` | End of while body |
| `}` | End of main |

## Common Traps
- ❌ Overflow if n is large (i*n could exceed int range)
- ❌ Wrong format string (must match exactly: `" x "` and `" = "`)
- ❌ Not printing newline after each line
- ❌ Forgetting to include putnbr prototype
- ❌ Using av[0] instead of av[1] (av[0] is program name)

## Related Exercises
- [[do_op]] - Calculator with putnbr
- [[print_hex]] - Number output with formatting
- [[ft_putnbr]] - Recursive number printing

## Wiki Links
03_Exams/Level_3_INDEX|Level 3 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 73 lines)
