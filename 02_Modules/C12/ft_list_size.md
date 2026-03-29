---
tags: []
date: 2026-03-29
status: complete
---
# ft_list_size

---
tags: [C12, red]
---

## Navigation
← C12_INDEX|C12 INDEX | [[ft_list_last|Next: ft_list_last →]]

## What it does
Counts and returns the number of elements in the linked list.

## The Insight
Traverse the list from head to tail, counting nodes until you reach NULL.

## Step-by-step Algorithm
1. Start from the first element (`begin_list`).
2. Initialize a counter to 0.
3. Iterate through the list: while current element is not NULL, increment counter and move to next.
4. Return the counter.
