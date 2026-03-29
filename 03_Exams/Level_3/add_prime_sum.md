---
tags: [Level_3, exam]
Level: 3
Topic: Algorithms
Exercise: add_prime_sum
---


# add_prime_sum

## What It Does
Sums all prime numbers from 2 to n, prints the sum.

## The Insight
Need `is_prime` helper function. For each number 2 to n, check if prime, add to sum. Use sqrt for efficient prime checking.

## Step-by-Step Algorithm
1. `n = atoi(av[1])`
2. `sum = 0`
3. Loop `i` from 2 to n: if `is_prime(i)`, `sum += i`
4. Print sum
5. `is_prime`: loop `j` from 2 to `sqrt(i)`, if `i%j==0` return 0, else return 1
6. Print newline

## Code
```c
int is_prime(int n)                              // Helper: checks if n is prime
{
    int i = 2;                                   // Start checking from 2

    while (i * i <= n)                          // Only need to check up to sqrt(n)
    {
        if (n % i == 0)                          // If n is divisible by i
            return 0;                            // n is not prime
        i++;                                     // Check next possible divisor
    }

    return n >= 2 ? 1 : 0;                       // Return 1 if prime (n >= 2), else 0
}

int main(int ac, char **av)                      // Main: argument count and argument vector
{
    int n = atoi(av[1]);                         // Parse number from argument
    int sum = 0;                                 // Initialize sum to 0
    int i = 2;                                   // Start checking from 2

    while (i <= n)                              // Loop from 2 to n
    {
        if (is_prime(i))                        // If i is prime
            sum += i;                            // Add i to sum
        i++;                                     // Move to next number
    }

    print_hex(sum);                              // Print sum using hex printing function
    write(1, "\n", 1);                          // Print final newline
}
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int is_prime(int n)` | Define helper function: checks if n is prime |
| `{` | Start of is_prime body |
| `int i = 2;` | Start checking divisors from 2 |
| `while (i * i <= n)` | Only need to check up to sqrt(n) |
| `if (n % i == 0)` | If n is divisible by i |
| `return 0;` | n is not prime |
| `i++;` | Check next possible divisor |
| `return n >= 2 ? 1 : 0;` | Return 1 if prime (and n>=2), else 0 |
| `}` | End of is_prime |
| `int main(int ac, char **av)` | Main function |
| `{` | Start of main body |
| `int n = atoi(av[1]);` | Parse number from argument |
| `int sum = 0;` | Initialize sum accumulator |
| `int i = 2;` | Start from 2 |
| `while (i <= n)` | Loop from 2 to n |
| `if (is_prime(i))` | If i is prime |
| `sum += i;` | Add i to sum |
| `i++;` | Move to next number |
| `print_hex(sum);` | Print sum using hex function |
| `write(1, "\n", 1);` | Print final newline |
| `}` | End of main |

## Common Traps
- ❌ Not handling 0 or 1 (should print 0, as neither is prime)
- ❌ Not using efficient sqrt check (checking all numbers up to n is too slow)
- ❌ Overflow in sum (especially for large n)
- ❌ Forgetting newline at the end

## Related Exercises
- [[fprime]] - Prime factorization
- [[print_hex]] - Hexadecimal output

## Wiki Links
03_Exams/Level_3_INDEX|Level 3 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 54 lines)
