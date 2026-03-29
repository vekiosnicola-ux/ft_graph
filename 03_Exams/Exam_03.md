---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# Exam 03 - Overview

---
tags: [Exams, magenta]
---


## Structure
- **Duration:** 2 hours
- **Levels:** 0-4
- **Points:** ~45-50 points

## Level 0-3
See [[Exam_00]], [[Exam_01]], [[Exam_02]] for Level 0-3 exercises.

## Level 4 (4 points each)
Complex algorithms and recursion.

| Exercise | Key Concept | Link |
|----------|-------------|------|
| flood_fill | Recursive fill | Level_4/flood_fill |
| fprime | Prime factorization | Level_4/fprime |
| ft_itoa | Integer to string | Level_4/ft_itoa |
| ft_list_foreach | List iteration | Level_4/ft_list_foreach |
| ft_list_remove_if | List filtering | Level_4/ft_list_remove_if |
| ft_split | String splitting | Level_4/ft_split |
| rev_wstr | Word reversal | Level_4/rev_wstr |
| rostring | Rotate string | Level_4/rostring |
| sort_int_tab | Array sorting | Level_4/sort_int_tab |
| sort_list | List sorting | Level_4/sort_list |

## Key Patterns
```c
// Flood fill recursive
void flood_fill(char **tab, t_point size, t_point begin, char target)
{
    if (begin.x < 0 || begin.x >= size.x || begin.y < 0 || begin.y >= size.y)
        return;
    if (tab[begin.y][begin.x] != target)
        return;
    tab[begin.y][begin.x] = 'F';
    flood_fill(tab, size, (t_point){begin.x - 1, begin.y}, target);
    flood_fill(tab, size, (t_point){begin.x + 1, begin.y}, target);
    flood_fill(tab, size, (t_point){begin.x, begin.y - 1}, target);
    flood_fill(tab, size, (t_point){begin.x, begin.y + 1}, target);
}
```

What is the flood fill algorithm?
::
1. Check bounds and target match
2. Mark current cell
3. Recursively fill 4 directions (up, down, left, right)

How does ft_itoa handle INT_MIN?
::
Convert to `long long` before negating to avoid overflow: `n = -(long long)nb`

## Dataview Query
```dataview
TABLE file.name as Exercise
FROM "03_Exams/Level_4"
SORT file.name ASC
```
