---
tags: []
date: 2026-03-29
status: complete
---
# ft_list_find

---
tags: [C12, red]
---

## Navigation
← C12_INDEX|C12 INDEX | [[ft_list_remove_if|Next: ft_list_remove_if →]]

## What it does
Returns a pointer to the first element whose `data` matches the `data_ref` using `cmp` for comparison.

## The Insight
Traverse list comparing each node's data with data_ref using cmp function.

## Step-by-step Algorithm
1. Start from the first element.
2. Iterate through the list:
   a. If `cmp(data, data_ref)` returns 0, return the current element.
   b. Move to the next element.
3. Return NULL if no match is found.
