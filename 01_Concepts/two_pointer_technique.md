---
tags: [Concepts]
---


# Two Pointer Technique

## What It Is
The two pointer technique uses two indices that traverse an array or string, often moving toward each other (from opposite ends) or in coordinated patterns. Enables O(n) solutions for problems that would otherwise require O(n²) nested loops, like reversing arrays, finding pairs, or palindrome checks.

## Key Points
- **Oppposite ends**: start at beginning and end, move toward center
- **Same direction**: both start at beginning, one moves faster (sliding window)
- **Coordinated movement**: adjust both based on conditions
- Reduces time complexity from O(n²) to O(n) for many problems
- Commonly used in: palindrome check, reverse array, two-sum (sorted), removing duplicates

## Related Concepts
- [[two_pointer_technique]]
- [[ft_rev_int_tab]]
- [[ft_strcmp]]

## Examples
```c
// Check if string is palindrome
int is_palindrome(char *str) {
    int left = 0;
    int right = 0;
    while (str[right] != '\0')
        right++;
    right--;  // back up from null terminator
    
    while (left < right) {
        if (str[left] != str[right])
            return 0;
        left++;
        right--;
    }
    return 1;
}

// Reverse array in place (O(n/2) swaps)
void reverse_array(int *arr, int size) {
    int left = 0;
    int right = size - 1;
    
    while (left < right) {
        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
        left++;
        right--;
    }
}

// Find pair with target sum in sorted array (O(n))
int find_pair(int *arr, int size, int target, int *a, int *b) {
    int left = 0;
    int right = size - 1;
    
    while (left < right) {
        int sum = arr[left] + arr[right];
        if (sum == target) {
            *a = arr[left];
            *b = arr[right];
            return 1;
        } else if (sum < target) {
            left++;
        } else {
            right--;
        }
    }
    return 0;
}
```

## Common Mistakes
- ❌ Off-by-one errors: not decrementing right initially to skip null terminator for strings
- ❌ Forgetting to move both pointers in each iteration
- ❌ Using wrong loop condition (`<=` vs `<`) causing extra comparison
