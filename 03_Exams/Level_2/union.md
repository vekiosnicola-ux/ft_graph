---
tags: [Level_2, exam]
  - memorization
Level: 2
Topic: Algorithms
Exercise: union
---


# union

## What It Does
Prints all DIFFERENT characters that appear in EITHER str1 or str2, with no duplicates, followed by newline.

## The Insight
Same memorization array as inter, but print AND mark on FIRST appearance from BOTH strings. Unlike inter, we NEVER unmark after printing.

## Step-by-Step Algorithm
1. `int seen[256]={0}` — create memorization array
2. Iterate str1: if `seen[str1[i]]==0`, print and set to 1
3. Iterate str2: same
4. Print newline

## Code
```c
int seen[256] = {0};                            // Memorization array: 256 bytes, all initialized to 0
int i = 0;                                      // String index variable

while (av[1][i])                               // First pass: process str1
{
    if (!seen[(unsigned char)av[1][i]])          // If character not seen before (not marked)
    {
        write(1, &av[1][i], 1);                 // Print the character
        seen[(unsigned char)av[1][i]] = 1;      // Mark as seen (set to 1, NEVER unset)
    }
    i++;                                         // Move to next character
}

i = 0;                                          // Reset index to 0
while (av[2][i])                               // Second pass: process str2
{
    if (!seen[(unsigned char)av[2][i]])          // If character not seen before
    {
        write(1, &av[2][i], 1);                 // Print the character
        seen[(unsigned char)av[2][i]] = 1;      // Mark as seen
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
| `while (av[1][i])` | Loop through first string (str1) |
| `if (!seen[(unsigned char)av[1][i]])` | If this character hasn't been printed yet |
| `write(1, &av[1][i], 1);` | Print the character |
| `seen[(unsigned char)av[1][i]] = 1;` | Mark character as seen (set to 1) |
| `}` | End of if block |
| `i++;` | Move to next character |
| `}` | End of first while loop |
| `i = 0;` | Reset index to 0 |
| `while (av[2][i])` | Loop through second string (str2) |
| `if (!seen[(unsigned char)av[2][i]])` | If character not seen before |
| `write(1, &av[2][i], 1);` | Print the character |
| `seen[(unsigned char)av[2][i]] = 1;` | Mark as seen |
| `}` | End of if block |
| `i++;` | Move to next character |
| `}` | End of second while loop |
| `write(1, "\n", 1);` | Print final newline |

## Common Traps
- ❌ Unmarking after printing (causes duplicates in output)
- ❌ Forgetting to check `seen[]` before printing
- ❌ Not processing both strings
- ❌ Forgetting the newline at the end

## Related Exercises
- [[inter]] - Intersection of two strings (only chars appearing in BOTH)
- [[wdmatch]] - Sequential character matching

## Wiki Links
03_Exams/Level_2_INDEX|Level 2 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 76 lines)
