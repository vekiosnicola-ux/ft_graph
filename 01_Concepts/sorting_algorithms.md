---
tags: [Concepts]
---


# Sorting Algorithms

## What It Is
Detailed explanations of major sorting algorithms with their characteristics. Each algorithm represents a different approach to the problem of ordering elements, with distinct tradeoffs between time complexity, space usage, and stability.

## Key Points
- **Bubble Sort**: O(n²), in-place, stable, simple but slow
- **Selection Sort**: O(n²), in-place, unstable, fewer swaps than bubble
- **Insertion Sort**: O(n²) worst/average, O(n) best, stable, efficient for small/nearly sorted
- **Merge Sort**: O(n log n) always, not in-place, stable, requires O(n) extra space
- **Quick Sort**: O(n log n) average, O(n²) worst, in-place, unstable

## Related Concepts
- [[sorting]]
- [[bubble_sort]]
- [[odometer_algorithm]]

## Examples
```c
// Bubble Sort - repeatedly swap adjacent if out of order
void bubble_sort(int *arr, int size) {
    for (int i = 0; i < size - 1; i++) {
        for (int j = 0; j < size - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                int temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
}

// Selection Sort - find minimum, place at beginning
void selection_sort(int *arr, int size) {
    for (int i = 0; i < size - 1; i++) {
        int min_idx = i;
        for (int j = i + 1; j < size; j++) {
            if (arr[j] < arr[min_idx])
                min_idx = j;
        }
        if (min_idx != i) {
            int temp = arr[i];
            arr[i] = arr[min_idx];
            arr[min_idx] = temp;
        }
    }
}

// Insertion Sort - build sorted portion one element at a time
void insertion_sort(int *arr, int size) {
    for (int i = 1; i < size; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}
```

## Common Mistakes
- ❌ Using bubble sort for anything but learning (too slow)
- ❌ Confusing stable vs unstable sorts when relative order matters
- ❌ Not handling edge cases (empty array, single element)
