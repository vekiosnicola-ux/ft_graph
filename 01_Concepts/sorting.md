---
tags: [Concepts]
---


# Sorting

## What It Is
Sorting is the process of arranging elements in a specific order (typically ascending or descending). It's a fundamental operation in computer science with numerous algorithms, each with different time/space tradeoffs. Choice of algorithm depends on data size, memory constraints, and whether data is already partially sorted.

## Key Points
- Sorting enables efficient searching (binary search requires sorted data)
- In-place sorting uses O(1) extra space; others require O(n)
- Stable sorts preserve relative order of equal elements
- Time complexity ranges from O(n log n) to O(n²)
- For small arrays (< 10-20 elements), O(n²) algorithms often beat O(n log n)

## Related Concepts
- [[sorting_algorithms]]
- [[bubble_sort]]
- [[bubble_sort]]
- [[odometer_algorithm]]

## Examples
```c
// Example: checking if array is sorted
int is_sorted(int *arr, int size) {
    for (int i = 0; i < size - 1; i++) {
        if (arr[i] > arr[i + 1])
            return 0;  // not sorted
    }
    return 1;  // sorted
}

// Finding minimum in unsorted array (O(n))
int find_min(int *arr, int size) {
    int min_val = arr[0];
    for (int i = 1; i < size; i++) {
        if (arr[i] < min_val)
            min_val = arr[i];
    }
    return min_val;
}
```

## Common Mistakes
- ❌ Using O(n²) algorithms for large datasets without considering performance
- ❌ Not accounting for stable vs unstable sorting when relative order matters
- ❌ Assuming sorted data remains sorted after insertion (requires re-sorting)
