---
tags: [Level_3, exam]
  - euclidean-algorithm
  - white
Level: 3
Topic: Algorithms
Exercise: pgcd
---


# pgcd

## What It Does
Prints the Greatest Common Divisor of two numbers passed as command-line arguments, followed by newline.

## The Insight
Euclidean algorithm. Repeatedly apply: `gcd(a,b) = gcd(b, a%b)` until `b==0`. When b is 0, a is the GCD.

## Step-by-Step Algorithm
1. `a = atoi(av[1])`, `b = atoi(av[2])`
2. While `b != 0`: `temp = b`; `b = a % b`; `a = temp`
3. Print a
4. Print newline

## Code
```c
int main(int ac, char **av)                      // Main: argument count and argument vector
{
    int a = atoi(av[1]);                         // Parse first number from argument 1
    int b = atoi(av[2]);                         // Parse second number from argument 2

    while (b)                                     // While b is not zero
    {
        int t = b;                                // Store current b in temporary variable
        b = a % b;                                // Compute remainder: a divided by b
        a = t;                                    // Set a to the previous b value
    }

    putnbr(a);                                    // Print the GCD (now stored in a)
    write(1, "\n", 1);                           // Print final newline
}
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int main(int ac, char **av)` | Main function with argument count and argument vector |
| `{` | Start of main body |
| `int a = atoi(av[1]);` | Parse first number from argument 1 |
| `int b = atoi(av[2]);` | Parse second number from argument 2 |
| `while (b)` | Loop while b is not zero |
| `{` | Start of while body |
| `int t = b;` | Store current b in temporary variable |
| `b = a % b;` | Compute remainder of a divided by b |
| `a = t;` | Set a to the previous b value |
| `}` | End of while body |
| `putnbr(a);` | Print the GCD value (now stored in a) |
| `write(1, "\n", 1);` | Print final newline |
| `}` | End of main |

## Common Traps
- ❌ Division by zero (when one number is 0, GCD is the other number)
- ❌ Forgetting newline at the end
- ❌ Wrong order in modulo (must be `a % b`, not `b % a`)
- ❌ Not handling negative numbers correctly

## Related Exercises
- [[lcm]] - Least Common Multiple (uses GCD internally)
- [[is_power_of_2]] - Related mathematical bit trick

## Wiki Links
03_Exams/Level_3_INDEX|Level 3 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 49 lines)
