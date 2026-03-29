---
tags: [Level_3, exam]
  - recursion
  - white
Level: 3
Topic: Algorithms
Exercise: print_hex
---


# print_hex

## What It Does
Converts a decimal number (as string) to hexadecimal and prints it.

## The Insight
First atoi the string to get the number, then use recursion like putnbr but with base 16. Modulo 16 gives the last hex digit, divide by 16 to advance.

## Step-by-Step Algorithm
1. `n = atoi(av[1])` — convert string to number
2. Recursive helper: if `n >= 16`, recurse with `n / 16`
3. Print hex digit using `"0123456789abcdef"[n % 16]`
4. Print newline

## Code
```c
void print_hex(unsigned int n)                   // Recursive hex printing function
{
    if (n >= 16)                                 // If n has more than one hex digit
        print_hex(n / 16);                        // Recursively print all digits except last

    write(1, &"0123456789abcdef"[n % 16], 1);    // Print last hex digit using string lookup
}

int main(int ac, char **av)                      // Main: argument count and argument vector
{
    if (ac == 2)                                 // Check that exactly one argument is given
        print_hex(atoi(av[1]));                  // Convert and print as hex
    write(1, "\n", 1);                           // Print final newline
}
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `void print_hex(unsigned int n)` | Define recursive hex printing function |
| `{` | Start of print_hex body |
| `if (n >= 16)` | If n has more than one hex digit |
| `print_hex(n / 16);` | Recursively call with n divided by 16 |
| `write(1, &"0123456789abcdef"[n % 16], 1);` | Print last digit using string indexing |
| `}` | End of print_hex |
| `int main(int ac, char **av)` | Main function |
| `{` | Start of main body |
| `if (ac == 2)` | Check exactly one argument provided |
| `print_hex(atoi(av[1]));` | Convert argument to int, then print as hex |
| `write(1, "\n", 1);` | Print final newline |
| `}` | End of main |

## Common Traps
- ❌ Not handling 0 (would print nothing without the recursive check)
- ❌ Trying to convert string directly to hex (must first convert string to number)
- ❌ Forgetting newline at the end
- ❌ Using unsigned instead of signed (avoids issues with large numbers)
- ❌ Forgetting to check argument count

## Related Exercises
- [[ft_atoi_base]] - Custom base conversion
- [[ft_putnbr]] - Recursive number printing
- [[add_prime_sum]] - Uses print_hex

## Wiki Links
03_Exams/Level_3_INDEX|Level 3 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 47 lines)
