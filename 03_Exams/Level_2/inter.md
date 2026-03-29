---
tags: [Level_2, exam]
  - memorization
Level: 2
Topic: Algorithms
Exercise: inter
---


# inter

## What It Does
Prints characters that appear in BOTH str1 and str2, with no duplicates, followed by newline.

## The Insight
Memorization using a 256-element int array. Mark chars seen in str2, print if marked when found in str1, then immediately unmark to prevent duplicates.

## Step-by-Step Algorithm
1. `int seen[256]={0}` — create memorization array
2. Iterate str2, set `seen[str2[i]]=1`
3. Iterate str1: if `seen[str1[i]]==1`, print and set `seen[str1[i]]=0`
4. Print newline

## Code
```c
int seen[256] = {0};                            // Memorization array: 256 ints, all initialized to 0
int i = 0;                                      // String index variable

while (av[2][i])                               // First pass: mark characters found in str2
{
    seen[(unsigned char)av[2][i]] = 1;           // Set seen[str2[i]] to 1 (present in str2)
    i++;                                         // Move to next character
}

i = 0;                                          // Reset index to 0
while (av[1][i])                               // Second pass: find characters in str1 that are also in str2
{
    if (seen[(unsigned char)av[1][i]] == 1)     // If character was marked as present in str2
    {
        write(1, &av[1][i], 1);                  // Print the character
        seen[(unsigned char)av[1][i]] = 0;      // UNMARK immediately to prevent duplicates
    }
    i++;                                         // Move to next character
}

write(1, "\n", 1);                              // Print newline at end of output
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int seen[256] = {0};` | Create 256-element array initialized to 0 |
| `int i = 0;` | Initialize string index variable |
| `while (av[2][i])` | Loop through second string (str2) |
| `seen[(unsigned char)av[2][i]] = 1;` | Mark character as present in str2 |
| `i++;` | Move to next character |
| `}` | End of first while loop |
| `i = 0;` | Reset index to 0 |
| `while (av[1][i])` | Loop through first string (str1) |
| `if (seen[(unsigned char)av[1][i]] == 1)` | If character was also in str2 (marked as present) |
| `write(1, &av[1][i], 1);` | Print the character |
| `seen[(unsigned char)av[1][i]] = 0;` | UNMARK to prevent printing duplicates |
| `}` | End of if block |
| `i++;` | Move to next character |
| `}` | End of second while loop |
| `write(1, "\n", 1);` | Print final newline |

## Common Traps
- ❌ Printing duplicates (must unmark after printing each character)
- ❌ Not using unsigned char for array index (negative char values)
- ❌ Not handling special characters outside ASCII range
- ❌ Forgetting the newline at the end

## Related Exercises
- [[union]] - Union of two strings (prints from BOTH, no duplicates)
- [[wdmatch]] - Sequential character matching

## Wiki Links
03_Exams/Level_2_INDEX|Level 2 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 74 lines)
