---
tags: [C01, flashcard]
---


# ft_div_mod

## What it does
Computes division and modulo, stores results via pointers.

## The Insight
Pointers let a function "return" multiple values by writing to caller's variables.

## Step-by-step Algorithm
1. Receive `int a, b` and `int *div, *mod`
2. Check `b != 0`
3. `*div = a / b`
4. `*mod = a % b`

## The Code (with pedagogical comments)
```c
void ft_div_mod(int a, int b, int *div, int *mod)  // Function: takes two ints and two pointers
{
    if (b != 0)  // Check for division by zero
    {
        *div = a / b;  // Dereference div and store the quotient
        *mod = a % b;  // Dereference mod and store the remainder
    }
}
```

## Line-by-Line Translation
1. `void ft_div_mod(int a, int b, int *div, int *mod)` - Define a function that takes two integers and two pointers to integers
2. `if (b != 0)` - Check if divisor is not zero (avoid division by zero)
3. `*div = a / b` - Compute integer division and store result through the div pointer
4. `*mod = a % b` - Compute remainder and store result through the mod pointer

## Common Traps
- ❌ Forgetting to dereference pointers (using `div = a / b` changes pointer, not value)
- ❌ Not checking for division by zero
- ❌ Using `int *div, *mod` without checking they are valid pointers

## Related Concepts
- 01_Concepts/pointers|Pointers
- 01_Concepts/multiple_return_values|Multiple Return Values

## Related Exercises
- [[ft_swap]]
- [[ft_ultimate_div_mod]]

## Propedeuticity
**Prerequisites:** [[ft_swap]]
**Unlocks:** [[ft_ultimate_div_mod]]

How do you return two values from one function?
::
Use pointers to write results back to the caller's variables:
```c
*div = a / b;  // Store quotient through pointer
*mod = a % b;  // Store remainder through pointer
```
