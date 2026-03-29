---
tags: []
date: 2026-03-29
status: complete
---
# ft_show_tab

---
tags: [C11, red]
---

## What it does
Displays the contents of a `t_stock_str` array, one element per line.

## Step-by-step Algorithm
1. Receive `t_stock_str *par`.
2. Iterate until `par[i].str == 0`.
3. For each element:
   - Print `par[i].str` using `write`.
   - Print newline.
   - Print `par[i].copy` using `write`.
   - Print newline.
   - Print `par[i].size` using `ft_putnbr`.
   - Print newline.

## The Code
```c
 <unistd.h>  // Provides write() for output

void ft_putnbr(int nb);  // Forward declaration: print integer

// Display all fields of each structure in the array
void ft_show_tab(struct s_stock_str *par)  // par = pointer to array of structures
{
    int i;  // Array index
    int j;  // Character index within a string

    i = 0;  // Start with first element in array
    while (par[i].str)  // While current element is NOT the sentinel (NULL end marker)
    {
        j = 0;  // Reset to first character of string
        while (par[i].str[j])  // While not at end of original string
            write(1, &par[i].str[j++], 1);  // Write one char, then increment j
        write(1, "\n", 1);  // Print newline after original string
        ft_putnbr(par[i].size);  // Print the size (integer) field
        write(1, "\n", 1);  // Print newline after size
        j = 0;  // Reset to first character again
        while (par[i].copy[j])  // While not at end of duplicated string
            write(1, &par[i].copy[j++], 1);  // Write one char, then increment j
        write(1, "\n", 1);  // Print newline after copy
        i++;  // Move to next structure in array
    }
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 22 | `#include <unistd.h>` | Header for write() system call |
| 26 | `void ft_show_tab(struct s_stock_str *par)` | Takes pointer to structure array |
| 28 | `int i;` | Index for structures in array |
| 29 | `int j;` | Index for characters in string |
| 31 | `i = 0;` | Start at first structure |
| 32 | `while (par[i].str)` | Sentinel loop: continue until str field is NULL (end marker) |
| 34 | `j = 0;` | Reset character index for string traversal |
| 35 | `while (par[i].str[j])` | Loop while not at null terminator |
| 36 | `write(1, &par[i].str[j++], 1);` | Write one char; j++ returns old value then increments |
| 37 | `write(1, "\n", 1);` | Newline after original string |
| 38 | `ft_putnbr(par[i].size);` | Print the integer size field |
| 39 | `write(1, "\n", 1);` | Newline after size |
| 41 | `j = 0;` | Reset for the copy string |
| 42-43 | (copy printing loop) | Print the duplicated string character by character |
| 44 | `write(1, "\n", 1);` | Newline after copy |
| 45 | `i++;` | Advance to next structure in array |

## Common Traps
- ❌ Forgetting to print all fields.
- ❌ Not looping until `str == 0`.
- ❌ Forgetting newlines between elements.
- ❌ Not initializing `j` properly in each loop iteration.

## Related Concepts
- 01_Concepts/structures|Structures
- 01_Concepts/write_syscall|write() syscall
