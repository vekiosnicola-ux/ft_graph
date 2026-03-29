---
tags: []
date: 2026-03-29
status: complete
---
# Bubble Sort

---
tags: [Concepts, blue]
---

## The Algorithm

Bubble sort repeatedly steps through the list, compares adjacent elements, and swaps them if they're in the wrong order. Larger elements "bubble up" to the end.

## Why It's Called Bubble Sort

The largest element bubbles up to the end in each pass, like air rising through water.

## Basic Implementation

From C01 ex08 `ft_sort_int_tab`:

```c
void ft_sort_int_tab(int *tab, int size)
{
    int i;
    int temp;
    
    i = 0;
    while (i < size - 1)
    {
        if (tab[i] > tab[i + 1])
        {
            temp = tab[i];
            tab[i] = tab[i + 1];
            tab[i + 1] = temp;
            i = 0;  // Restart scan from beginning
        }
        else
            i++;
    }
}
```

## Step-by-Step Example

Array: `[5, 3, 8, 1]`

```
Pass 1: [5, 3, 8, 1] → compare 5,3 → swap → [3, 5, 8, 1]
        [3, 5, 8, 1] → compare 5,8 → no swap
        [3, 5, 8, 1] → compare 8,1 → swap → [3, 5, 1, 8]

Pass 2: [3, 5, 1, 8] → compare 3,5 → no swap
        [3, 5, 1, 8] → compare 5,1 → swap → [3, 1, 5, 8]
        [3, 1, 5, 8] → compare 5,8 → no swap

Pass 3: [3, 1, 5, 8] → compare 3,1 → swap → [1, 3, 5, 8]
        [1, 3, 5, 8] → compare 3,5 → no swap
        [1, 3, 5, 8] → compare 5,8 → no swap

Done! [1, 3, 5, 8]
```

## Why Reset i = 0?

After any swap, we restart from the beginning because:
1. The swapped element might now be smaller than elements before it
2. We need to re-check the entire array for each position

## Time Complexity

- Best: O(n) — already sorted
- Worst: O(n²) — reverse sorted
- Average: O(n²)

For n=10: at most 45 comparisons.

## Alternative: Track if Swapped

```c
void bubble_sort(int *tab, int size)
{
    int i;
    int swapped;
    int temp;
    
    while (1)
    {
        swapped = 0;
        i = 0;
        while (i < size - 1)
        {
            if (tab[i] > tab[i + 1])
            {
                temp = tab[i];
                tab[i] = tab[i + 1];
                tab[i + 1] = temp;
                swapped = 1;
            }
            i++;
        }
        if (!swapped)
            break;  // No swaps means sorted
    }
}
```

This optimizes best-case from O(n²) to O(n).

## Why Bubble Sort in 42?

Bubble sort is simple and guaranteed to work. Other algorithms (quicksort, mergesort) are more efficient but more complex. The exercise tests:
- Array manipulation
- Nested loops (or single loop with reset)
- Swapping with temporary variable

## Key Takeaway

Bubble sort is the simplest sorting algorithm:
1. Compare adjacent elements
2. Swap if wrong order
3. Repeat until no swaps needed
4. Restart from beginning after each swap

It demonstrates core array manipulation concepts without the complexity of advanced algorithms.

---

**Related:** [[invisible_skeleton]], [[pointers]], [[malloc]]
