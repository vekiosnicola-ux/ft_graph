---
tags: []
date: 2026-03-29
status: complete
---
# ft_list_remove_if

---
tags: [C12, red]
---

## Navigation
← C12_INDEX|C12 INDEX

## What it does
Removes all elements where `cmp(data, data_ref)` returns 0. Frees the memory of removed elements.

## The Insight
Track previous pointer to relink list when removing nodes. Save next before freeing.

## Step-by-step Algorithm
1. Keep a previous pointer to track the element before the current one.
2. Iterate through the list:
   a. If `cmp(current->data, data_ref)` returns 0:
      - Link previous->next to current->next.
      - Free current's data and element.
      - Move current to next.
   b. Otherwise, update previous to current and move forward.
