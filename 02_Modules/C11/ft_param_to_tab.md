---
tags: []
date: 2026-03-29
status: complete
---
# ft_param_to_tab

---
tags: [C11, red]
---

## What it does
Converts command-line arguments into an array of `t_stock_str` structures.

## Step-by-step Algorithm
1. Define `t_stock_str` with `size`, `str`, `copy` fields.
2. Receive `int ac`, `char **av`.
3. Allocate array: `malloc((ac + 1) * sizeof(t_stock_str))`.
4. For each argument:
   - `size = ft_strlen(av[i])`
   - `str = av[i]`
   - `copy = ft_strdup(av[i])`
5. Set last element to empty structure.
6. Return the array.

## The Code
```c
 <stdlib.h>  // Provides malloc() and free()

// Structure to hold information about a string
typedef struct s_stock_str
{
    int size;    // Length of the string (number of characters)
    char *str;   // Pointer to the original string
    char *copy;  // Pointer to a duplicate (copy) of the string
} t_stock_str;   // Type alias: struct s_stock_str now called t_stock_str

// Calculate string length by counting characters until '\0'
int ft_strlen(char *str)
{
    int i;  // Character position counter

    i = 0;  // Start at first character
    while (str[i])  // While current character is not null terminator
        i++;  // Count this character and move to next
    return (i);  // Return total number of characters
}

// Duplicate a string by allocating new memory and copying contents
char *ft_strdup(char *src)  // Returns pointer to newly allocated copy
{
    char *dest;  // Pointer to destination (new copy) buffer
    int i;       // Index for copying characters

    dest = malloc(ft_strlen(src) + 1);  // Allocate: length of src + 1 for '\0'
    if (!dest)  // Check if malloc failed
        return (NULL);  // Signal failure
    i = 0;  // Start copying from first character
    while (src[i])  // While source has not reached null terminator
    {
        dest[i] = src[i];  // Copy each character to destination
        i++;  // Advance both indices
    }
    dest[i] = '\0';  // Explicitly terminate destination string
    return (dest);  // Return pointer to the new copy
}

// Convert command-line arguments into an array of stock_str structures
t_stock_str *ft_param_to_tab(int ac, char **av)  // ac=arg count, av=arg vector
{
    t_stock_str *tab;  // Pointer to output array of structures
    int i;             // Loop index for iterating through arguments

    tab = malloc((ac + 1) * sizeof(t_stock_str));  // Allocate: ac strings + 1 sentinel
    if (!tab)  // Check if allocation succeeded
        return (NULL);  // Exit with failure
    i = 0;  // Start processing arguments from index 0
    while (i < ac)  // Process each argument (0 to ac-1)
    {
        tab[i].size = ft_strlen(av[i]);  // Store length of this argument
        tab[i].str = av[i];               // Point to original argument string
        tab[i].copy = ft_strdup(av[i]);  // Create and store a duplicate copy
        i++;  // Move to next argument
    }
    tab[i].size = 0;  // After all real data: set sentinel (empty element)
    tab[i].str = 0;   // Null pointer for sentinel
    tab[i].copy = 0;  // Null pointer for sentinel
    return (tab);  // Return pointer to the populated structure array
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 24 | `typedef struct s_stock_str {...} t_stock_str;` | Define structure with 3 fields; alias as t_stock_str |
| 31 | `int ft_strlen(char *str)` | Count characters until null terminator |
| 41 | `char *ft_strdup(char *src)` | Create independent copy of string |
| 46 | `dest = malloc(ft_strlen(src) + 1);` | Allocate exact bytes needed plus null terminator |
| 55 | `dest[i] = '\0';` | Manually terminate the copied string |
| 59 | `t_stock_str *ft_param_to_tab(...)` | Convert argv array to structure array |
| 64 | `tab = malloc((ac + 1) * sizeof(t_stock_str));` | +1 for sentinel NULL-terminating element |
| 68 | `tab[i].size = ft_strlen(av[i]);` | Calculate and store length of argument i |
| 69 | `tab[i].str = av[i];` | Store pointer directly to original argument |
| 70 | `tab[i].copy = ft_strdup(av[i]);` | Create and store independent duplicate copy |
| 75-77 | (sentinel) | Mark the end of array with empty/zero element |

## Common Traps
- ❌ Forgetting to allocate for the NULL terminator element.
- ❌ Forgetting to check malloc return.
- ❌ Not setting the last element to empty/zero.
- ❌ Not duplicating the string.

## Related Concepts
- 01_Concepts/structures|Structures
- 01_Concepts/malloc|malloc/free
