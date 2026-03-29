---
tags: []
date: 2026-03-29
status: complete
---
# ft_list_map

---
tags: [C12, red]
---

## Navigation
← C12_INDEX|C12 INDEX | [[ft_list_find|Next: ft_list_find →]]

## What it does
Creates a new list by applying function `f` to each element's `data` in the original list. The new list is returned.

## The Insight
Create new nodes with transformed data, preserving list structure.

## Step-by-step Algorithm
1. If `begin_list` is NULL, return NULL.
2. Create the first new element with `f(begin_list->data)`.
3. Store the head of the new list.
4. Iterate through original list, creating new elements and linking them.
5. Return the head of the new list.
