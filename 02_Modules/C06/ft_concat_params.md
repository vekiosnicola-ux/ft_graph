---
tags: [C06]
---


# ft_concat_params

## What it Does
Concatenates command-line arguments into a single string, separated by newlines.

## The Insight
Calculate total length, allocate memory, then copy each argument followed by '\n' (except the last).

## Step-by-step Algorithm
1. Count `argc` and iterate through `argv` to calculate total length.
2. Allocate `malloc(total_length + 1)`.
3. Copy each argument into the result string, adding '\n' after each (except last).
4. Null-terminate the string.
5. Return the result.

## The Code
```c
 <stdlib.h> // Provides malloc() for dynamic memory allocation

// Main function: concatenate command-line arguments with newlines between them
char *ft_concat_params(int argc, char **argv)
{
    char *result;       // Pointer to the concatenated string (will be returned)
    char *ptr;         // Moving pointer to track where to write next
    int i;              // Loop counter for iterating through arguments (strings)
    int j;              // Loop counter for iterating through each character
    int len;            // Total length of all arguments plus newlines

    i = 1;              // Start at 1: argv[0] is the program name, skip it
    len = 0;            // Start length counter at 0
    while (i < argc)    // Loop through all arguments (argv[1] to argv[argc-1])
    {
        j = 0;          // Reset j to start of current argument
        while (argv[i][j])  // Count characters in this argument
            len++, j++;     // Increment len and move to next character
        if (i < argc - 1)   // If NOT the last argument, add newline after it
            len++;          // Account for the newline character
        i++;                // Move to next argument
    }                      // len now equals total characters + newlines
    result = malloc(len + 1);  // Allocate memory for all chars + null terminator
    if (!result)           // Check for malloc failure
        return (NULL);     // Propagate error
    ptr = result;          // ptr tracks current write position
    i = 1;                 // Reset i to skip program name again
    while (i < argc)       // Copy each argument into result
    {
        j = 0;              // Reset j to start of current argument
        while (argv[i][j])  // Copy all characters of current argument
            *ptr++ = argv[i][j++];  // Copy char and advance both pointers
        if (i < argc - 1)   // If NOT the last argument, add newline
            *ptr++ = '\n';  // Write newline character
        i++;                // Move to next argument
    }
    *ptr = '\0';            // Null-terminate the final string
    return (result);        // Return the concatenated string
}
```

## Line-by-Line Translation
- `include <stdlib.h>` — Header for malloc() and free()
- `char *ft_concat_params(int argc, char **argv)` — Concatenate program arguments
- `i = 1;` — Start at index 1 (skip argv[0] which is the program name)
- `len = 0;` — Initialize total length to zero
- `while (i < argc)` — Loop through all arguments
- `while (argv[i][j]) len++, j++;` — Count characters in each argument
- `if (i < argc - 1) len++;` — Add 1 for newline between arguments
- `result = malloc(len + 1);` — Allocate exact memory needed
- `ptr = result;` — Use ptr as the write position tracker
- `*ptr++ = argv[i][j++];` — Copy each character, advancing pointers
- `if (i < argc - 1) *ptr++ = '\n';` — Add newline between arguments
- `*ptr = '\0';` — Null-terminate the result
- `return (result);` — Return the concatenated string

## Common Traps
- ❌ Forgetting to skip `argv[0]` (program name).
- ❌ Forgetting the null terminator.
- ❌ Not counting newlines between arguments.
- ❌ Forgetting to free the result after use.

## Related
- ex03 ft_strjoin
