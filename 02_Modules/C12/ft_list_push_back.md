---
tags: []
date: 2026-03-29
status: complete
---
# ft_list_push_back

---
tags: [C12, red]
---

## Navigation
← C12_INDEX|C12 INDEX | [[ft_list_clear|Next: ft_list_clear →]]

## What it does
Adds a new element at the end of the list.

## The Insight
Traverse to the last node, then set its `next` to the new element.

## Step-by-step Algorithm
1. Create a new element using `ft_create_elem`.
2. If `*begin_list` is NULL, set the new element as the first element.
3. Otherwise, traverse to the last element and set its `next` to the new element.
