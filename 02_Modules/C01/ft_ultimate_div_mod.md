---
tags: [C01, flashcard]
---


# ft_ultimate_div_mod

## What it does
Divides two integers, stores quotient in first and remainder in second, both via pointers.

## The Insight
Need temp to store original `*a` before overwriting. Performs div_mod AND swap in-place.

## Step-by-step Algorithm
1. Receive `int *a, *b`
2. Check `*b != 0`
3. Store `*a` in `temp_a`
4. `*a = temp_a / *b`
5. `*b = temp_a % *b`

## The Code (with pedagogical comments)
```c
void ft_ultimate_div_mod(int *a, int *b)  // Function: takes two pointers to integers
{
    int temp_a;  // Temporary variable to save original value of *a

    if (*b != 0)  // Check for division by zero
    {
        temp_a = *a;  // Save the original value at address a
        *a = temp_a / *b;  // Store the quotient at address a
        *b = temp_a % *b;  // Store the remainder at address b
    }
}
```

## Line-by-Line Translation
1. `void ft_ultimate_div_mod(int *a, int *b)` - Define a function that takes two pointers to integers
2. `int temp_a` - Declare a temporary variable to hold the original value of *a
3. `if (*b != 0)` - Check if the value at address b is not zero
4. `temp_a = *a` - Save the value at address a into temp_a
5. `*a = temp_a / *b` - Compute quotient and store at address a
6. `*b = temp_a % *b` - Compute remainder and store at address b

## Common Traps
- ❌ Using `*a` directly before storing it (would lose original value)
- ❌ Forgetting to dereference pointers
- ❌ Not checking for division by zero

## Related Concepts
- 01_Concepts/pointers|Pointers
- 01_Concepts/division_modulo|Division and Modulo

## Related Exercises
- [[ft_div_mod]]
- [[ft_swap]]

## Propedeuticity
**Prerequisites:** [[ft_div_mod]], [[ft_swap]]
**Unlocks:** C02 string exercises

Why do you need temp_a?
::
To preserve the original value of *a before overwriting it with the quotient.
```c
temp_a = *a;  // Save first
*a = temp_a / *b;  // Now we can use original value for division
*b = temp_a % *b;  // And for modulo
```
