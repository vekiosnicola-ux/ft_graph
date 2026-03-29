---
tags: [Level_3, exam]
  - recursion
  - white
Level: 3
Topic: Algorithms
Exercise: paramsum
---


# paramsum

## What It Does
Prints the number of additional arguments passed (`argc - 1`), followed by newline. Must handle multi-digit numbers.

## The Insight
Simple `argc` minus 1. But must print multi-digit numbers, so use recursive putnbr to handle any integer value.

## Step-by-Step Algorithm
1. `count = argc - 1`
2. Use recursive putnbr to print count (handles multi-digit)
3. Print newline

## Code
```c
void putnbr(int n)                               // Recursive number printing function
{
    if (n < 0)                                   // Handle negative numbers
    {
        write(1, "-", 1);                        // Print negative sign
        n = -n;                                  // Make n positive for processing
    }

    if (n >= 10)                                 // If more than one digit
        putnbr(n / 10);                         // Recursively print all digits except last

    // Print the last/final digit using string indexing
    write(1, &"0123456789"[n % 10], 1);
}

int main(int ac, char **av)                      // Main: argument count and argument vector
{
    putnbr(ac - 1);                              // Print (argc - 1): number of additional args
    write(1, "\n", 1);                          // Print final newline
}
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `void putnbr(int n)` | Define recursive number printing function |
| `{` | Start of putnbr body |
| `if (n < 0)` | Check if number is negative |
| `{` | Start of negative handling |
| `write(1, "-", 1);` | Print negative sign |
| `n = -n;` | Negate n to make it positive |
| `}` | End of negative handling |
| `if (n >= 10)` | If n has more than one digit |
| `putnbr(n / 10);` | Recursively call with n/10 (all digits except last) |
| `write(1, &"0123456789"[n % 10], 1);` | Print last digit using string lookup |
| `}` | End of putnbr |
| `int main(int ac, char **av)` | Main function with argument count and vector |
| `{` | Start of main body |
| `putnbr(ac - 1);` | Print argc minus 1 (number of additional args) |
| `write(1, "\n", 1);` | Print final newline |
| `}` | End of main |

## Common Traps
- ❌ Not handling multi-digit numbers (can't just print `argc + '0'`)
- ❌ Forgetting newline at the end
- ❌ Forgetting to handle negative numbers (though argc-1 is rarely negative)
- ❌ Not using recursion (iterative approach also works but recursion is elegant here)

## Related Exercises
- [[ft_putnbr]] - Recursive number printing
- [[print_hex]] - Base conversion output

## Wiki Links
03_Exams/Level_3_INDEX|Level 3 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 54 lines)
