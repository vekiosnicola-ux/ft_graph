---
tags: [C01, flashcard]
---


# ft_ft

## Navigation
← C01_INDEX|C01 INDEX | [[ft_ultimate_ft|Next: ft_ultimate_ft →]]

## What it does
Sets the integer pointed to by `nbr` to 42.

## The Insight
`*nbr` accesses the value at the memory address. `*nbr = 42` modifies the original variable.

## Step-by-step Algorithm
1. Receive `int *nbr`
2. Dereference: `*nbr`
3. Assign 42

## The Code (with pedagogical comments)
```c
void ft_ft(int *nbr)  // Function: returns nothing, takes pointer to int
{
    *nbr = 42;  // Dereference pointer and assign 42 to the value at that address
}
```

## Line-by-Line Translation
1. `void ft_ft(int *nbr)` - Define a function that returns nothing and takes a pointer to an integer
2. `*nbr = 42` - Dereference the pointer (access the value at the address) and set it to 42

## Common Traps
- ❌ `nbr = 42` would change the pointer, not the value
- ❌ Passing non-pointer (compilation error)

## Related Concepts
- 01_Concepts/pointers|Pointers

## Related Exercises
- [[ft_ultimate_ft]]
- [[ft_swap]]

## Propedeuticity
**Prerequisites:** C00 exercises
**Unlocks:** [[ft_swap]], [[ft_ultimate_ft]]

What does `*nbr = 42` do?
::
Dereferences the pointer and sets the VALUE at that address to 42
