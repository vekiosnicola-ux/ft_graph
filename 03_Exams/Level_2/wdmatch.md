---
tags: [Level_2, exam]
Level: 2
Topic: String Manipulation
Exercise: wdmatch
---


# wdmatch

## What It Does
Checks if characters from str1 can form str2 IN ORDER. If yes, prints str1. If no, prints nothing. Both followed by newline.

## The Insight
Single-pointer walk through str2, advancing through str1 whenever there's a match. At the end, if str1 was fully consumed, it matches.

## Step-by-Step Algorithm
1. Initialize `idx=0` for str1 position tracker
2. Iterate `i` through str2
3. If `str2[i]==str1[idx]`, increment idx
4. After loop, if `str1[idx]=='\0'`, print str1
5. Always print newline

## Code
```c
int i = 0, idx = 0;                             // i=str2 index, idx=str1 position tracker

while (av[2][i] && av[1][idx])                 // Loop while both strings have characters
{
    if (av[2][i] == av[1][idx])                 // If current characters match
        idx++;                                    // Advance str1 tracker to next char
    i++;                                         // Always advance through str2
}

if (av[1][idx] == '\0')                         // If we matched all of str1 (reached end)
{
    i = 0;                                       // Reset i to print str1 from beginning
    while (av[1][i])                            // Loop through entire str1
    {
        write(1, &av[1][i], 1);                  // Write each character
        i++;                                     // Move to next character
    }
}

write(1, "\n", 1);                              // Print final newline
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int i = 0, idx = 0;` | Initialize indices: i for str2, idx for str1 progress |
| `while (av[2][i] && av[1][idx])` | Loop while both strings have characters remaining |
| `if (av[2][i] == av[1][idx])` | Check if current characters match |
| `idx++;` | Advance str1 tracker when characters match |
| `i++;` | Always advance through str2 |
| `}` | End of while loop |
| `if (av[1][idx] == '\0')` | Check if we consumed all of str1 (match success) |
| `{` | Start of print block |
| `i = 0;` | Reset i to print str1 from beginning |
| `while (av[1][i])` | Loop through entire str1 |
| `write(1, &av[1][i], 1);` | Write each character |
| `i++;` | Move to next character |
| `}` | End of inner while loop |
| `}` | End of if block |
| `write(1, "\n", 1);` | Print final newline |

## Common Traps
- ❌ Printing "OK" or "yes" instead of printing str1 itself
- ❌ Forgetting to check if `str1[idx]=='\0'` at end
- ❌ Printing wrong string (should print av[1], not av[2])
- ❌ Not printing anything when match fails (should still print newline)

## Related Exercises
- [[hidenp]] - Similar character-in-sequence check
- [[inter]] - Character set intersection

## Wiki Links
03_Exams/Level_2_INDEX|Level 2 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 73 lines)
