---
tags: []
date: 2026-03-29
status: complete
---
# ft_sort_params

---
tags: [C11, red]
---

## Navigation
← C11_INDEX|C11 INDEX

## What it does
Sorts command-line arguments in ASCII order and prints them, one per line.

## Step-by-step Algorithm
1. Receive `int argc` and `char **argv`.
2. Sort `argv[1]` to `argv[argc-1]` using a simple sorting algorithm (bubble sort).
3. Compare strings using `ft_strcmp`.
4. Swap pointers if needed.
5. Print each argument on a new line.

## The Code
```c
 <unistd.h>  // Provides write() for output

// Compare two strings: returns negative if s1 < s2, 0 if equal, positive if s1 > s2
int ft_strcmp(char *s1, char *s2)
{
    int i;  // Index for character-by-character comparison

    i = 0;  // Start at first character of both strings
    while (s1[i] && s2[i] && s1[i] == s2[i])  // While chars match and neither string ended
        i++;  // Move to next character position
    return (s1[i] - s2[i]);  // Return difference: 0 if equal, + if s1 > s2, - if s1 < s2
}

// Swap two string pointers (swap where they point in memory)
void ft_swap(char **a, char **b)  // Takes pointers to string pointers
{
    char *temp;  // Temporary storage for one pointer

    temp = *a;  // Save where a points
    *a = *b;    // Make a point where b pointed
    *b = temp;  // Make b point to saved location
}

int main(int argc, char **argv)  // Program entry: argc=count, argv=string array
{
    int i;  // Outer loop index for sorting
    int j;  // Inner loop index for comparison

    i = 1;  // Start at first command-line argument (skip program name at argv[0])
    while (i < argc - 1)  // Bubble sort: compare argv[i] with all subsequent elements
    {
        j = i + 1;  // Start comparing with element after i
        while (j < argc)  // Compare argv[i] with argv[j] for all j > i
        {
            if (ft_strcmp(argv[i], argv[j]) > 0)  // If argv[i] should come after argv[j]
                ft_swap(&argv[i], &argv[j]);  // Swap the pointers so smaller string is first
            j++;  // Check next element
        }
        i++;  // Move to next position in the sorted region
    }
    // Now print all arguments in sorted order
    i = 1;  // Reset to first argument (skip program name)
    while (i < argc)  // Loop through all arguments
    {
        while (*argv[i])  // While not at end of string (until '\0')
            write(1, argv[i]++, 1);  // Write one character, then advance pointer
        write(1, "\n", 1);  // Print newline after each argument
        i++;  // Move to next argument
    }
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 20 | `int ft_strcmp(char *s1, char *s2)` | Compare two strings lexicographically |
| 22 | `int i;` | Character position index |
| 24 | `i = 0;` | Start comparing from first character |
| 25 | `while (s1[i] && s2[i] && s1[i] == s2[i])` | Loop while characters match and strings haven't ended |
| 26 | `i++;` | Move to next character |
| 27 | `return (s1[i] - s2[i]);` | Return ASCII difference at first differing position |
| 30 | `void ft_swap(char **a, char **b)` | Swap where two char pointers point |
| 32 | `char *temp;` | Holding spot for one pointer |
| 34 | `temp = *a;` | Save a's target address |
| 35 | `*a = *b;` | Point a to b's target |
| 36 | `*b = temp;` | Point b to saved address |
| 39 | `int main(int argc, char **argv)` | Program entry with command-line arguments |
| 44 | `i = 1;` | Skip argv[0] (program's own name) |
| 45 | `while (i < argc - 1)` | Outer loop: bubble sort through arguments |
| 47 | `j = i + 1;` | Inner loop starts at next element |
| 50 | `if (ft_strcmp(argv[i], argv[j]) > 0)` | If string i should come after string j |
| 51 | `ft_swap(&argv[i], &argv[j]);` | Swap their positions in array |
| 57 | `i = 1;` | Reset to print sorted results |
| 59-62 | (print loop) | Print each argument character by character |

## Common Traps
- ❌ Forgetting to skip `argv[0]` (program name).
- ❌ Not comparing correctly with `ft_strcmp`.
- ❌ Not printing newline after each argument.
