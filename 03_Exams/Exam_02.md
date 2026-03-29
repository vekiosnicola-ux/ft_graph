---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# Exam 02 - Overview

---
tags: [Exams, magenta]
---


## Structure
- **Duration:** 2 hours
- **Levels:** 0-3
- **Points:** ~35-40 points

## Level 0-2
See [[Exam_00]] and [[Exam_01]] for Level 0-2 exercises.

## Level 3 (3 points each)
Advanced algorithms and data structures.

| Exercise | Key Concept | Link |
|----------|-------------|------|
| add_prime_sum | Prime numbers | Level_3/add_prime_sum |
| epur_str | String cleaning | Level_3/epur_str |
| expand_str | String expansion | Level_3/expand_str |
| ft_atoi_base | Base conversion | Level_3/ft_atoi_base |
| ft_list_size | Linked list | Level_3/ft_list_size |
| ft_range | Array allocation | Level_3/ft_range |
| ft_rrange | Reverse range | Level_3/ft_rrange |
| hidenp | Hidden pattern | Level_3/hidenp |
| lcm | Least common multiple | Level_3/lcm |
| paramsum | Parameter sum | Level_3/paramsum |
| pgcd | GCD calculation | Level_3/pgcd |
| print_hex | Hex printing | Level_3/print_hex |
| rstr_capitalizer | Reverse capitalizer | Level_3/rstr_capitalizer |
| str_capitalizer | String capitalizer | Level_3/str_capitalizer |
| tab_mult | Table multiplication | Level_3/tab_mult |

## Key Patterns
```c
// LCM using GCD (Euclidean algorithm)
int gcd(int a, int b)
{
    while (b)
    {
        int temp = b;
        b = a % b;
        a = temp;
    }
    return (a);
}

int lcm(int a, int b)
{
    return (a * b / gcd(a, b));
}
```

How do you calculate LCM?
::
`lcm(a, b) = (a * b) / gcd(a, b)` where GCD uses Euclidean algorithm

What is the ft_range algorithm?
::
1. Calculate size: `abs(max - min)`
2. Allocate: `malloc(size * sizeof(int))`
3. Fill array from min to max

## Dataview Query
```dataview
TABLE file.name as Exercise
FROM "03_Exams/Level_3"
SORT file.name ASC
```
