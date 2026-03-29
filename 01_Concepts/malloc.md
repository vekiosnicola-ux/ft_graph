---
tags: []
date: 2026-03-29
status: complete
---
# malloc: Dynamic Memory Allocation

---
tags: [Concepts, blue]
---

## What malloc Does

`malloc` (memory allocation) requests a block of bytes from the operating system. It returns the **starting address** of that block.

```c
 <stdlib.h>

void *malloc(size_t size);
```

- `size`: Number of **bytes** to allocate
- Returns: Starting address, or `NULL` if failed

## Memory Regions

```
Stack                    Heap
[f局部变量]              [malloc数据]
    ↓                      ↑
    └──── grow toward ─────┘
```

- **Stack**: Automatic, fixed size, fast
- **Heap**: Dynamic, can grow, requires `malloc`/`free`

## Basic Usage

```c
// Allocate 5 integers (5 * 4 = 20 bytes)
int *arr = malloc(5 * sizeof(int));

if (arr == NULL)
    return;  // Allocation failed

// Use arr...
arr[0] = 10;
arr[4] = 50;

free(arr);  // Return memory to system
```

## ft_range: Complete malloc Example

From C06 ex00 `ft_range`:

```c
int *ft_range(int start, int end)
{
    int size;
    int *range;
    int i;
    
    size = abs(end - start);  // How many integers?
    range = malloc(size * sizeof(int));  // Allocate
    
    if (range == NULL)
        return NULL;
    
    i = 0;
    if (start < end)
    {
        while (start < end)
            range[i++] = start++;
    }
    else
    {
        while (start > end)
            range[i++] = start--;
    }
    return range;
}
```

## ft_strdup: Copying Strings

From textbook `ft_strdup`:

```c
char *ft_strdup(char *src)
{
    int len = 0;
    char *copy;
    
    while (src[len] != '\0')  // Find string length
        len++;
    
    copy = malloc(len + 1);  // +1 for \0
    if (copy == NULL)
        return NULL;
    
    len = 0;
    while (src[len] != '\0')  // Copy bytes
    {
        copy[len] = src[len];
        len++;
    }
    copy[len] = '\0';  // Don't forget terminator!
    
    return copy;
}
```

## Common malloc Mistakes

### 1. Forgetting +1 for Null Terminator

```c
char *s = malloc(5);  // ❌ Only 5 bytes
strcpy(s, "Hello");   // Writes 6 bytes (including \0)
// Buffer overflow!
```

### 2. Not Checking for NULL

```c
int *p = malloc(1000000 * sizeof(int));
*p = 42;  // ❌ CRASH if malloc returned NULL
```

### 3. Off-by-One in Size Calculation

```c
// For an array of n elements:
int *arr = malloc(n * sizeof(int));  // ✅ Correct
int *arr = malloc(n * sizeof(int) + 1);  // ❌ Wasteful
int *arr = malloc((n - 1) * sizeof(int));  // ❌ Too small
```

### 4. Forgetting to free()

```c
void leak_example(void)
{
    int *p = malloc(sizeof(int));
    *p = 42;
    return;  // ❌ Memory leak - p is gone but memory isn't
}
```

## sizeof: Getting Byte Size

```c
sizeof(int)     // Usually 4 bytes
sizeof(char)    // Always 1 byte
sizeof(char *)  // Pointer size (4 or 8 depending on arch)
```

## ft_split: Complex malloc

From textbook Level 4 exercise:

```c
// Splits "hello world" into ["hello", "world"]
char **ft_split(char *str)
{
    // Count words first
    int words = count_words(str);
    
    // Allocate array of pointers (+1 for NULL terminator)
    char **result = malloc((words + 1) * sizeof(char *));
    
    // For each word, allocate memory for the word + \0
    // Copy the word into each allocated space
    
    result[words] = NULL;  // NULL-terminate the array
    return result;
}
```

## Memory Alignment

`malloc` returns addresses aligned for any data type. You don't need to worry about alignment.

## Key Takeaway

`malloc` requests dynamic memory from the heap. Always:
1. Calculate size correctly (don't forget `\0` for strings)
2. Check for `NULL` return
3. `free()` when done
4. Never use `free()` on non-malloc'd memory

---

**Related:** [[pointers]], [[null_terminator]], [[invisible_skeleton]], [[linked_lists]]
