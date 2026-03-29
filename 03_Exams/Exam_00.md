---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# Exam 00 - Overview

---
tags: [Exams, magenta]
---


## Structure
- **Duration:** 2 hours
- **Levels:** 0-1
- **Points:** ~15-20 points

## Level 0 (1 point each)
Basic output and simple transformations.

| Exercise | Key Concept | Link |
|----------|-------------|------|
| hello | Basic output | Level_0/hello |
| aff_a | Character search | Level_0/aff_a |
| aff_first_param | Argument handling | Level_0/aff_first_param |
| aff_last_param | Argument handling | Level_0/aff_last_param |
| aff_z | Character output | Level_0/aff_z |
| only_a | Character filtering | Level_0/only_a |
| only_z | Character filtering | Level_0/only_z |
| maff_alpha | Alphabet manipulation | Level_0/maff_alpha |
| maff_revalpha | Reverse alphabet | Level_0/maff_revalpha |
| ft_print_numbers | Number output | Level_0/ft_print_numbers |
| ft_countdown | Countdown loop | Level_0/ft_countdown |

## Level 1 (1 point each)
String manipulation and basic algorithms.

| Exercise | Key Concept | Link |
|----------|-------------|------|
| fizzbuzz | Conditional logic | Level_1/fizzbuzz |
| first_word | String parsing | Level_1/first_word |
| ft_strlen | String length | Level_1/ft_strlen |
| ft_putstr | String output | Level_1/ft_putstr |
| ft_swap | Pointer swap | Level_1/ft_swap |
| ft_strcpy | String copy | Level_1/ft_strcpy |
| rev_print | Reverse print | Level_1/rev_print |
| rot_13 | Caesar cipher | Level_1/rot_13 |
| rotone | Single rotation | Level_1/rotone |
| ulstr | Case inversion | Level_1/ulstr |
| repeat_alpha | Alpha repetition | Level_1/repeat_alpha |
| search_and_replace | Character replacement | Level_1/search_and_replace |

## Key Patterns
```c
// The Invisible Skeleton (80% of Level 0-1)
int i = 0;
while (str[i] != '\0')
{
    do_something();
    i++;
}
```

What is the "invisible skeleton" pattern?
::
1. Initialize: `int i = 0;`
2. Loop: `while (str[i] != '\0')`
3. Action + Increment: `do_something(); i++;`

How do you print a character using write?
::
`write(1, &c, 1)` - pass the ADDRESS (&c), not the value

## Dataview Query
```dataview
TABLE file.name as Exercise
FROM "03_Exams/Level_0" OR "03_Exams/Level_1"
SORT file.name ASC
```
