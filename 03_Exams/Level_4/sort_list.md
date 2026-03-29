---
tags: [Level_4, exam]
  - linked-list
  - sorting
  - white
---


# sort_list

## What it does
Sorts linked list in ascending order using bubble sort logic (swap data, not pointers).

## The Insight
ONLY swap ->data, NEVER try to swap ->next pointers (causes lost nodes). Reset to head after each swap.

## Step-by-step Algorithm
1. While not sorted: reset to head
2. Compare current and next
3. If out of order, swap data
4. Move to next
5. Repeat

## The Code
```c
// sort_list: Sorts linked list using bubble sort on data
// Takes: pointer to list head, comparison function cmp(a,b) returns >0 if a>b
// IMPORTANT: Only swaps DATA, never rearranges pointers

void sort_list(t_list **begin_list, int (*cmp)())
{
    t_list *cur = *begin_list;             // Current node during traversal
    int swapped;                           // Flag: did we swap anything this pass?
    char *temp;                            // Temporary storage for swapping data
    
    while (1)                              // Outer loop: keep sorting until no swaps
    {
        swapped = 0;                        // Reset swap flag for this pass
        cur = *begin_list;                  // Reset to head of list
        while (cur->next)                   // Inner loop: while not at last node
        {
            if ((*cmp)(cur->data, cur->next->data) > 0)  // If current > next (out of order)
            {
                temp = cur->data;            // Save current's data
                cur->data = cur->next->data; // Copy next's data to current
                cur->next->data = temp;      // Write saved data to next
                swapped = 1;                  // Mark that we made a swap
            }
            cur = cur->next;                 // Move to next node
        }
        if (!swapped)                        // If no swaps in this pass
            break;                           // List is sorted, exit
    }
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 22 | `void sort_list(t_list **begin_list, int (*cmp)())` | Takes double pointer to list head, function pointer for comparison |
| 24 | `t_list *cur = *begin_list;` | Current node pointer initialized to head |
| 25 | `int swapped;` | Flag variable: 1 if we swapped this pass, 0 otherwise |
| 26 | `char *temp;` | Temporary pointer for swapping data pointers |
| 27 | `while (1)` | Outer loop: keep passes until sorted |
| 29 | `swapped = 0;` | Reset swapped flag at start of each pass |
| 30 | `cur = *begin_list;` | Reset current to head for new pass |
| 31 | `while (cur->next)` | Inner loop: traverse until last node (can't compare after last) |
| 33 | `if ((*cmp)(cur->data, cur->next->data) > 0)` | Call comparison function: if cur > next |
| 35 | `temp = cur->data;` | Step 1 of 3-way swap: save current's data pointer |
| 36 | `cur->data = cur->next->data;` | Step 2: copy next's data to current |
| 37 | `cur->next->data = temp;` | Step 3: write saved data to next node |
| 38 | `swapped = 1;` | Mark that a swap occurred this pass |
| 40 | `cur = cur->next;` | Advance to next node |
| 42-43 | `if (!swapped) break;` | If no swaps this pass, list is sorted |

## Common Traps
- ❌ Trying to swap ->next pointers (causes lost nodes, broken links, infinite loops - NEVER do this)
- ❌ Not resetting to head after swap (would miss checking earlier elements in next pass)
- ❌ Wrong comparison function (cmp should return >0 if first > second)

## Related
- [[sort_int_tab]] - array sorting
- [[ft_list_remove_if]] - list removal
- EXAMS INDEX|Exam INDEX
