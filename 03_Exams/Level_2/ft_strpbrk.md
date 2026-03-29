---
tags: [Level_2, exam]
Level: 2
Topic: String Manipulation
Exercise: ft_strpbrk
---


# ft_strpbrk

## What It Does
Returns pointer to the first char in s1 that matches any char in s2. Returns NULL if none found.

## The Insight
Nested skeleton loops. Outer loop through s1, inner loop through s2 for each character.

## Step-by-Step Algorithm
1. Iterate `i` through s1 until '\0'
2. For each `s1[i]`, iterate `j` through s2
3. If match found, return `&s1[i]`
4. If no match in all of s1, return NULL

## Code
```c
int i = 0, j;                                     // i=s1 index, j=s2 index

while (s1[i])                                     // Loop through s1 until null terminator
{
    j = 0;                                        // Reset s2 index to check from beginning
    while (s2[j])                                 // Loop through s2 looking for match
    {
        if (s1[i] == s2[j])                       // If s1[i] matches any char in s2
            return &s1[i];                         // Return pointer to that character in s1
        j++;                                       // Check next char in s2
    }
    i++;                                           // No match in s2, move to next char in s1
}
return NULL;                                       // Return NULL if no match found in entire s1
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int i = 0, j;` | Declare indices for s1 (i) and s2 (j) |
| `while (s1[i])` | Loop through s1 until null terminator |
| `{` | Start of outer while body |
| `j = 0;` | Reset s2 index to start for each s1 character |
| `while (s2[j])` | Loop through s2 looking for match with s1[i] |
| `{` | Start of inner while body |
| `if (s1[i] == s2[j])` | Check if characters match |
| `return &s1[i];` | Return pointer to matching character in s1 |
| `j++;` | Check next character in s2 |
| `}` | End of inner while loop |
| `i++;` | No match in s2, advance to next s1 character |
| `}` | End of outer while loop |
| `return NULL;` | Return NULL (no match found in s1) |

## Common Traps
- ❌ Returning char instead of pointer (wrong return type)
- ❌ Not checking `s1[i]=='\0'` (the outer while handles this)
- ❌ Forgetting to return NULL if no match found
- ❌ Not resetting j for each character in s1

## Related Exercises
- [[ft_strcspn]] - Complementary function (length of segment with no chars from s2)
- [[ft_strspn]] - Related string scanning
- [[hidenp]] - Sequential character matching

## Wiki Links
03_Exams/Level_2_INDEX|Level 2 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 72 lines)
