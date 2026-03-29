---
tags: [C06]
---


# ft_putnbr_fd

## What it Does
Outputs an integer to the given file descriptor.

## The Insight
Uses recursion to print digits in correct order. Handles negative by printing '-' and using `long long` to avoid overflow.

## Step-by-step Algorithm
1. Convert `n` to `long long` to safely handle INT_MIN.
2. If negative, write '-' and make `n` positive.
3. If `n >= 10`, recursively call with `n / 10`.
4. Write the last digit as a character.

## The Code
```c
 <unistd.h> // Provides the write() function for low-level I/O operations

void ft_putnbr_fd(int n, int fd) // Function takes an integer and a file descriptor
{                               // fd tells where to write (1 = stdout, 2 = stderr, etc.)
    long long nb;               // Use long long to safely handle INT_MIN (-2147483648)

    if (n < 0)                  // Check if the number is negative
    {
        write(fd, "-", 1);      // Write the minus sign to the specified file descriptor
        nb = -(long long)n;     // Convert to positive, casting to long long to prevent overflow
    }
    else                        // Number is zero or positive
        nb = n;                 // Store as-is (implicit conversion to long long)
    if (nb >= 10)               // If nb is 10 or greater, we need to print higher digits first
        ft_putnbr_fd(nb / 10, fd); // Recursively call with nb divided by 10 (removes last digit)
    nb = nb % 10 + '0';         // Get the last digit: remainder of nb / 10, convert to ASCII char
    write(fd, &nb, 1);          // Write the single digit character to the file descriptor
}                               // Recursion unwinds, printing digits from left to right
```

## Line-by-Line Translation
- `#include <unistd.h>` — Include the header for the write() system call
- `void ft_putnbr_fd(int n, int fd)` — Define a function that writes an integer to a file descriptor
- `long long nb;` — Declare a long long variable to safely handle all integer values
- `if (n < 0)` — Check if the original number is negative
- `write(fd, "-", 1);` — Output a minus sign to the specified file descriptor
- `nb = -(long long)n;` — Convert to positive long long (casting prevents overflow with INT_MIN)
- `else` — For zero and positive numbers
- `nb = n;` — Copy the value directly
- `if (nb >= 10)` — If we have two or more digits left to print
- `ft_putnbr_fd(nb / 10, fd);` — Recursively process all digits except the last one
- `nb = nb % 10 + '0';` — Extract last digit and convert to its ASCII character representation
- `write(fd, &nb, 1);` — Write the single character digit to the file descriptor

## Common Traps
- ❌ Not handling INT_MIN (overflow when negating).
- ❌ Forgetting to convert digit to character with + '0'.
- ❌ Recursing without base case (works because n < 10 stops).
- ❌ Using `printf` instead of `write`.

## Related
- ex07 ft_putchar_fd
- ex08 ft_putstr_fd
- ex09 ft_putendl_fd
