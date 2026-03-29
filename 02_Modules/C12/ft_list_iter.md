---
tags: []
date: 2026-03-29
status: complete
---
# ft_list_iter

---
tags: [C12, red]
---

## Navigation
← C12_INDEX|C12 INDEX | [[ft_list_map|Next: ft_list_map →]]

## What it does
Applies the function `f` to each element's `data` in the list.

## The Insight
Simple traversal: start at head, apply f to data, move to next until NULL.

## Step-by-step Algorithm
1. Start from the first element.
2. While current element is not NULL:
   a. Apply function `f` to `current->data`.
   b. Move to the next element.
