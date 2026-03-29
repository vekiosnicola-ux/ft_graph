---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# Exam 01 - Overview

---
tags: [Exams, magenta]
---


## Structure
- **Duration:** 2 hours
- **Levels:** 0-2
- **Points:** ~25-30 points

## Level 0-1
See [[Exam_00]] for Level 0-1 exercises (same pool).

## Level 2 (2 points each)
Intermediate algorithms and string operations.

| Exercise | Key Concept | Link |
|----------|-------------|------|
| alpha_mirror | Character mirroring | Level_2/alpha_mirror |
| camel_to_snake | Case conversion | Level_2/camel_to_snake |
| do_op | Arithmetic parsing | Level_2/do_op |
| ft_atoi | String to integer | Level_2/ft_atoi |
| ft_strcmp | String comparison | Level_2/ft_strcmp |
| ft_strcspn | String span | Level_2/ft_strcspn |
| ft_strdup | String duplication | Level_2/ft_strdup |
| ft_strpbrk | String search | Level_2/ft_strpbrk |
| ft_strrev | String reverse | Level_2/ft_strrev |
| ft_strspn | String span | Level_2/ft_strspn |
| inter | Character intersection | Level_2/inter |
| is_power_of_2 | Power check | Level_2/is_power_of_2 |
| last_word | Last word extraction | Level_2/last_word |
| max | Maximum value | Level_2/max |
| print_bits | Bit printing | Level_2/print_bits |
| reverse_bits | Bit reversal | Level_2/reverse_bits |
| snake_to_camel | Case conversion | Level_2/snake_to_camel |
| swap_bits | Bit swapping | Level_2/swap_bits |
| union | String union | Level_2/union |
| wdmatch | Word matching | Level_2/wdmatch |

## Key Patterns
```c
// ft_atoi pattern
while (str[i] == ' ' || str[i] == '\t')
    i++;
if (str[i] == '-' || str[i] == '+')
    sign = str[i++];
while (str[i] >= '0' && str[i] <= '9')
    result = result * 10 + (str[i++] - '0');
```

What is the ft_atoi algorithm?
::
1. Skip whitespace
2. Handle sign (+/-)
3. Accumulate digits: `result = result * 10 + (c - '0')`
4. Return result * sign

How does ft_strcmp work?
::
Compare characters one by one. Return the difference at the first mismatch. If all match, return 0.

## Dataview Query
```dataview
TABLE file.name as Exercise
FROM "03_Exams/Level_2"
SORT file.name ASC
```
