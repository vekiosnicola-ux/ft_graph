---
tags: [Level_3, exam]
  - subsequence
  - white
Level: 3
Topic: String Manipulation
Exercise: hidenp
---


# hidenp

## What It Does
Returns 1 if ALL characters of str1 appear IN ORDER in str2 (can be separated by other chars). Else returns 0.

## The Insight
Two-pointer approach. Walk through str2, when char matches current str1 char, advance str1 pointer. At the end, if str1 was fully consumed, return 1.

## Step-by-Step Algorithm
1. `i=0` (str1 index), `j=0` (str2 index)
2. While `str2[j]` and `str1[i]`: if `str2[j]==str1[i]`, `i++`
3. Always `j++`
4. If `str1[i]=='\0'`, return 1, else 0

## Code
```c
int hidenp(char *s1, char *s2)                   // Function: takes two strings, returns int
{
    int i = 0, j = 0;                           // i=str1 index, j=str2 index

    while (s2[j] && s1[i])                      // Loop while both strings have characters
    {
        if (s2[j] == s1[i])                      // If characters match
            i++;                                  // Advance str1 index (consume this char from s1)
        j++;                                     // Always advance through str2
    }

    // Return 1 if all chars of s1 were found (reached end), else 0
    return s1[i] == '\0' ? 1 : 0;
}
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int hidenp(char *s1, char *s2)` | Define function: two strings, returns int |
| `{` | Start of function body |
| `int i = 0, j = 0;` | Initialize indices: i for s1, j for s2 |
| `while (s2[j] && s1[i])` | Loop while both strings have characters remaining |
| `{` | Start of while body |
| `if (s2[j] == s1[i])` | Check if current characters match |
| `i++;` | Advance s1 index (consume matching char from s1) |
| `j++;` | Always advance through s2 |
| `}` | End of while body |
| `return s1[i] == '\0' ? 1 : 0;` | Return 1 if all s1 chars found (reached end), else 0 |
| `}` | End of function |

## Common Traps
- ❌ Empty s1 should return 1 (empty pattern matches everything)
- ❌ Characters must be in ORDER, not just present somewhere
- ❌ Not advancing i when match found (would miss the next char)
- ❌ Forgetting to always advance j

## Related Exercises
- [[wdmatch]] - Similar character-in-sequence check
- [[ft_strspn]] - Related string scanning

## Wiki Links
03_Exams/Level_3_INDEX|Level 3 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 49 lines)
