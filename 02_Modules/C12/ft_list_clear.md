---
tags: []
date: 2026-03-29
status: complete
---
# ft_list_clear

---
tags: [C12, red]
---

## Navigation
← C12_INDEX|C12 INDEX | [[ft_list_iter|Next: ft_list_iter →]]

## What it does
Frees all elements of the list and sets the list pointer to NULL.

## The Insight
Save next pointer before freeing current, then move forward. After freeing all, set head to NULL.

## Step-by-step Algorithm
1. Save the current element.
2. Move to the next element before freeing the current one.
3. Repeat until all elements are freed.
4. Set `*begin_list` to NULL.
