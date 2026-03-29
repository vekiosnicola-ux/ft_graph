---
tags: [C01, flashcard]
---


# ft_swap

## Navigation
← [[ft_ft|ft_ft]] | [[ft_ultimate_ft|Next: ft_ultimate_ft →]]

## What it does
Swaps two integers using pointers.

## The Insight
Pass pointers to modify original values. Use temp variable to avoid losing a value during swap.

## Step-by-step Algorithm
1. Receive `int *a`, `int *b`
2. Store `*a` in `temp`
3. Assign `*b` to `*a`
4. Assign `temp` to `*b`

## The Code (with pedagogical comments)
```c
void ft_swap(int *a, int *b)  // Function: takes two pointers to integers
{
    int temp;  // Temporary variable to hold one value during swap

    temp = *a;  // Store the value at address a into temp
    *a = *b;    // Put the value at address b into address a
    *b = temp;  // Put the stored temp value into address b
}
```

## Line-by-Line Translation
1. `void ft_swap(int *a, int *b)` - Define a function that takes two pointers to integers
2. `int temp` - Create a temporary variable to hold one value
3. `temp = *a` - Read the value at address a and store it in temp
4. `*a = *b` - Read the value at address b and write it to address a
5. `*b = temp` - Write the stored temp value to address b

## Common Traps
- ❌ Forgetting to dereference (using `a = b` instead of `*a = *b`)
- ❌ Not using temp (would lose one value)

## Related Concepts
- 01_Concepts/pointers|Pointers

## Related Exercises
- [[ft_ft]]
- [[ft_ultimate_ft]]
- [[ft_div_mod]]

## Propedeuticity
**Prerequisites:** [[ft_ft]]
**Unlocks:** [[ft_div_mod]], [[ft_ultimate_div_mod]]

How does ft_swap work?
::
```c
temp = *a;  // Save value at a
*a = *b;    // Copy value from b to a
*b = temp;  // Restore saved value to b
```
