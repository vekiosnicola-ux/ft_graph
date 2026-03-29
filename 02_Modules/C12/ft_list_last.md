---
tags: []
date: 2026-03-29
status: complete
---
# ft_list_last

---
tags: [C12, red]
---

## Navigation
← C12_INDEX|C12 INDEX | [[ft_list_push_front|Next: ft_list_push_front →]]

## What it does
Returns a pointer to the last element of the list.

## The Insight
Traverse the list until `next` is NULL - that's the last element.

## Step-by-step Algorithm
1. If the list is empty, return NULL.
2. Start from the first element.
3. Iterate through the list until `next` is NULL.
4. Return the current element (which is the last one).
