---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# Concept Mastery Tracker

---
tags: [Tracking, brown]
---

## Core Concepts

### Pointers
- **Status:** □□□□□
- **Key Exercises:** ft_ft, ft_ultimate_ft, ft_swap
- **Common Mistakes:** Forgetting to dereference, confusing & and *
- **Review:** [[pointers]]

### Strings
- **Status:** □□□□□
- **Key Exercises:** ft_strlen, ft_strcpy, ft_strcmp
- **Common Mistakes:** Forgetting null terminator, buffer overflow
- **Review:** [[null_terminator]]

### Memory
- **Status:** □□□□□
- **Key Exercises:** ft_memset, ft_memcpy, ft_strdup
- **Common Mistakes:** Memory leaks, buffer overflow
- **Review:** [[malloc]]

### Recursion
- **Status:** □□□□□
- **Key Exercises:** ft_putnbr, flood_fill, ft_print_memory
- **Common Mistakes:** No base case, stack overflow
- **Review:** [[recursion]]

### Linked Lists
- **Status:** □□□□□
- **Key Exercises:** ft_lstnew, ft_lstadd_front, ft_lstclear
- **Common Mistakes:** Memory leaks, NULL pointer dereference
- **Review:** [[linked_lists]]

### Binary Trees
- **Status:** □□□□□
- **Key Exercises:** btree_create_node, btree_insert_data
- **Common Mistakes:** Incorrect traversal order, memory leaks
- **Review:** [[binary_trees]]

## Algorithm Mastery

### Sorting
- **Status:** □□□□□
- **Key Exercises:** ft_sort_int_tab, sort_int_tab
- **Algorithm:** Bubble sort, merge sort
- **Review:** [[bubble_sort]]

### String Manipulation
- **Status:** □□□□□
- **Key Exercises:** ft_strcapitalize, ft_split
- **Common Mistakes:** Off-by-one errors, memory allocation
- **Review:** string_manipulation

### Bitwise Operations
- **Status:** □□□□□
- **Key Exercises:** print_bits, reverse_bits, swap_bits
- **Common Mistakes:** Operator precedence, sign extension
- **Review:** bitwise_operations

## Exam Readiness

### Level 0-1
- **Status:** □□□□□
- **Focus:** Basic output, string manipulation
- **Time:** 30 minutes

### Level 2
- **Status:** □□□□□
- **Focus:** ft_atoi, ft_strcmp, bitwise operations
- **Time:** 45 minutes

### Level 3
- **Status:** □□□□□
- **Focus:** ft_range, lcm, linked lists
- **Time:** 60 minutes

### Level 4
- **Status:** □□□□□
- **Focus:** flood_fill, ft_split, sorting
- **Time:** 90 minutes

### Level 5
- **Status:** □□□□□
- **Focus:** brackets, brainfuck, rpn_calc
- **Time:** 120 minutes

What are the 6 core concepts to master?
::
1. Pointers
2. Strings
3. Memory
4. Recursion
5. Linked Lists
6. Binary Trees

What is the recommended time allocation for each exam level?
::
- Level 0-1: 30 minutes
- Level 2: 45 minutes
- Level 3: 60 minutes
- Level 4: 90 minutes
- Level 5: 120 minutes

## Dataview Query
```dataview
TABLE
  choice(status = "□□□□□", "🆕 New",
    choice(status = "■□□□□", "📚 Developing",
      choice(status = "■■□□□", "✅ Competent",
        choice(status = "■■■□□", "⭐ Proficient",
          choice(status = "■■■■■", "🏆 Master", status))))) as Status
FROM "05_Tracking"
WHERE status
SORT file.name ASC
```
