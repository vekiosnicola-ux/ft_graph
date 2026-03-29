---
tags: [C06]
---


# ft_itoa

## What it Does
Converts an integer to a string representation.

## The Insight
Handle negative numbers separately, then extract digits recursively from right to left.

## Step-by-step Algorithm
1. Handle special case `n = -2147483648` (INT_MIN).
2. Calculate `len` (number of digits).
3. Allocate `malloc(len + 1)`.
4. If `n < 0`, handle sign and convert to positive.
5. Fill string from right to left using `n % 10`.
6. Add null terminator.
7. Return the string.

## The Code
```c
 <stdlib.h> // Provides malloc() for dynamic memory allocation and free()

// Helper function: returns the absolute value of n
// Handles INT_MIN specially to prevent overflow when negating
int ft_abs(int n)
{
    if (n < 0)         // If n is negative (including INT_MIN)
        return (-n);    // Negate it to get positive value
    return (n);         // Already positive, return as-is
}

// Helper function: counts how many digits are in n (including '-' for negatives)
int ft_count_digits(int n)
{
    int len;            // Will store the digit count

    if (n == 0)         // Special case: single digit zero
        return (1);     // "0" is one character
    len = 0;            // Start counting from 0
    if (n < 0)         // If number is negative
        len++;          // Account for the '-' sign in the final string
    while (n != 0)     // Keep dividing by 10 until nothing left
    {
        len++;          // Each division removes one digit
        n = n / 10;     // Integer division drops the last digit
    }                   // Example: 123 -> 12 -> 1 -> 0 (3 iterations)
    return (len);      // Return total characters needed
}

// Main function: converts an integer to a string
char *ft_itoa(int nbr)
{
    char *result;       // Pointer to the resulting string (will be returned)
    int len;            // Length of the string (number of characters)
    int n;              // Temporary variable to hold the number during processing

    if (nbr == -2147483648)                           // INT_MIN: special case!
        return (ft_strdup("-2147483648"));            // Cannot negate safely, handle as string
    len = ft_count_digits(nbr);                       // Calculate how many characters we need
    result = malloc(len + 1);                         // Allocate memory: len chars + null terminator
    if (!result)                                      // Check if malloc() failed (returns NULL)
        return (NULL);                                // Propagate NULL to indicate error
    result[len] = '\0';                               // Place null terminator at the END first
    if (nbr < 0)                                     // Handle negative numbers
    {
        result[0] = '-';                              // First character is the minus sign
        n = ft_abs(nbr);                              // Convert to positive for digit extraction
    }
    else
        n = nbr;                                      // For positive numbers, use as-is
    len--;                                           // Point to the last character position
    while (len >= 0 && result[len] != '-')            // Fill digits from RIGHT to LEFT
    {                                                // Stop if we hit the '-' sign (negative numbers)
        result[len] = '0' + (n % 10);                 // Convert last digit to character: 7 -> '7'
        n = n / 10;                                  // Remove the last digit from n
        len--;                                       // Move left to the previous position
    }                                                // Result: digits placed from end to start
    return (result);                                 // Return the newly created string
}
```

## Line-by-Line Translation
- `include <stdlib.h>` — Include for malloc() and free() for dynamic memory allocation
- `int ft_abs(int n)` — Helper function to compute absolute value
- `if (n < 0)` — Check if number is negative
- `return (-n);` — Negate and return (but careful with INT_MIN!)
- `int ft_count_digits(int n)` — Count characters needed to represent n
- `if (n == 0) return (1);` — Zero needs one digit
- `len = 0;` — Start counter at zero
- `if (n < 0) len++;` — Account for minus sign
- `while (n != 0)` — Loop until all digits are extracted
- `len++; n = n / 10;` — Count each digit, divide by 10 to shift
- `char *ft_itoa(int nbr)` — Main conversion function
- `if (nbr == -2147483648)` — Special case: INT_MIN cannot be safely negated
- `return (ft_strdup("-2147483648"));` — Return as hardcoded string
- `len = ft_count_digits(nbr);` — Calculate required string length
- `result = malloc(len + 1);` — Allocate len characters + null terminator
- `if (!result) return (NULL);` — Handle malloc failure
- `result[len] = '\0';` — Place null terminator at the end
- `if (nbr < 0)` — Handle negative numbers
- `result[0] = '-';` — Write minus sign first
- `n = ft_abs(nbr);` — Convert to positive value
- `while (len >= 0 && result[len] != '-')` — Fill digits backwards
- `result[len] = '0' + (n % 10);` — Convert digit to ASCII character
- `n = n / 10;` — Remove processed digit
- `return (result);` — Return the finished string

## Related
- C00 ex07 ft_putnbr
