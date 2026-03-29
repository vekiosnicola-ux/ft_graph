---
tags: [Level_2, exam]
Level: 2
Topic: String Manipulation
Exercise: ft_strrev
---


# ft_strrev

## What It Does
Reverses a string in place using two pointers (start and end).

## The Insight
Two-pointer approach. Swap characters from start and end, moving both pointers toward the middle until they meet.

## Step-by-Step Algorithm
1. Find string length
2. Set `start=0`, `end=len-1`
3. While `start<end`: swap chars, `start++`, `end--`

## Code
```c
int i = 0;                                        // First pass: find string length
while (str[i])                                    // Loop until null terminator
    i++;                                          // Count characters

int j = i - 1;                                    // j = last character index (length - 1)
i = 0;                                            // Reset i to 0 (start of string)

while (i < j)                                     // While start hasn't crossed end
{
    char temp = str[i];                            // Store character at start position
    str[i] = str[j];                              // Copy character from end to start
    str[j] = temp;                                // Copy stored start character to end
    i++;                                           // Move start index forward
    j--;                                           // Move end index backward
}
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int i = 0;` | Initialize index to 0 |
| `while (str[i])` | Loop until null terminator |
| `i++;` | Count each character |
| `int j = i - 1;` | Set j to last valid character index (length - 1) |
| `i = 0;` | Reset i to start of string |
| `while (i < j)` | While start hasn't crossed end |
| `{` | Start of while body |
| `char temp = str[i];` | Store character at start position |
| `str[i] = str[j];` | Copy end character to start position |
| `str[j] = temp;` | Copy stored start character to end position |
| `i++;` | Move start index forward |
| `j--;` | Move end index backward |
| `}` | End of while body |

## Common Traps
- ❌ Trying to reverse a string literal (read-only memory, causes segfault)
- ❌ Using `start<=end` instead of `start<end` (would swap middle char with itself)
- ❌ Not using a temporary variable for swapping
- ❌ Forgetting to find length first

## Related Exercises
- [[ft_print_comb]] - Nested loop pattern
- [[rev_print]] - Related reversal printing
- [[ft_rev_int_tab]] - Integer array reversal

## Wiki Links
03_Exams/Level_2_INDEX|Level 2 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 71 lines)
