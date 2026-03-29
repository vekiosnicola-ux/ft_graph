---
tags: [exam, flashcard]
date: 2026-03-29
status: complete
---
# Final Exam - Overview

---
tags:
  - 
  - white
---

## Structure
- **Duration:** 4 hours
- **Levels:** 0-5
- **Points:** ~60-70 points

## Level 0-4
See [[Exam_00]], [[Exam_01]], [[Exam_02]], [[Exam_03]] for Level 0-4 exercises.

## Level 5 (5+ points each)
Advanced programming challenges.

| Exercise | Key Concept | Link |
|----------|-------------|------|
| brackets | Bracket matching | Level_5/brackets |
| brainfuck | Brainfuck interpreter | Level_5/brainfuck |
| ft_itoa_base | Base conversion | Level_5/ft_itoa_base |
| options | Option parsing | Level_5/options |
| print_memory | Memory dump | Level_5/print_memory |
| rpn_calc | RPN calculator | Level_5/rpn_calc |

## Key Patterns
```c
// Bracket matching with stack
int check_brackets(char *str)
{
    char stack[100];
    int top = -1;
    
    while (*str)
    {
        if (*str == '(' || *str == '[' || *str == '{')
            stack[++top] = *str;
        else if (*str == ')' || *str == ']' || *str == '}')
        {
            if (top < 0 || !match(stack[top--], *str))
                return (0);
        }
        str++;
    }
    return (top == -1);
}
```

How does the RPN calculator work?
::
1. Use a stack
2. For each token:
   - If number: push to stack
   - If operator: pop 2 numbers, compute, push result
3. Return final stack value

What is the brainfuck instruction set?
::
- `>` `<` move pointer
- `+` `-` modify cell
- `.` output, `,` input
- `[` `]` loop (while cell != 0)

## Dataview Query
```dataview
TABLE file.name as Exercise
FROM "03_Exams/Level_5"
SORT file.name ASC
```
