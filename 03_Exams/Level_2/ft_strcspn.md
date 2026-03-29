---
tags: [Level_2, exam]
Level: 2
Topic: String Manipulation
Exercise: ft_strcspn
---


# ft_strcspn

## What It Does
Returns the length of the initial segment of s1 that contains NO characters from s2. (Complementary to ft_strspn.)

## The Insight
Similar to strpbrk but counting instead of returning pointer. For each char in s1, check if it exists anywhere in s2.

## Step-by-Step Algorithm
1. Iterate `i` through s1
2. For each `s1[i]`, check ALL chars in s2
3. If match found in s2, return current `i`
4. If none found until '\0', return `i` (full length)

## Code
```c
int i = 0, j;                                     // i=s1 index, j=s2 index

while (s1[i])                                     // Loop through s1 until null terminator
{
    j = 0;                                        // Reset s2 index to check from beginning
    while (s2[j])                                 // Loop through s2 looking for match
    {
        if (s1[i] == s2[j])                       // If s1[i] matches any char in s2
            return i;                              // Return current index (rejecting char found)
        j++;                                       // Check next char in s2
    }
    i++;                                           // No match in s2, move to next char in s1
}
return i;                                          // Return length (all chars were acceptable)
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int i = 0, j;` | Declare indices for s1 (i) and s2 (j) |
| `while (s1[i])` | Loop through s1 until null terminator |
| `{` | Start of while body |
| `j = 0;` | Reset s2 index to start for each s1 character |
| `while (s2[j])` | Loop through s2 looking for match with s1[i] |
| `{` | Start of inner while body |
| `if (s1[i] == s2[j])` | Check if characters match |
| `return i;` | Return current index (found forbidden char, stop here) |
| `j++;` | Check next character in s2 |
| `}` | End of inner while loop |
| `i++;` | No match in s2, advance to next s1 character |
| `}` | End of outer while loop |
| `return i;` | Return length (entire s1 has no chars from s2) |

## Common Traps
- ❌ Returning `j` instead of `i` (j is index in s2, not s1)
- ❌ Not checking all of s2 for each s1[i]
- ❌ Missing final return (when entire s1 is valid)
- ❌ Forgetting to reset j=0 for each character in s1

## Related Exercises
- [[ft_strspn]] - Opposite function (only chars from s2)
- [[ft_strpbrk]] - Returns pointer instead of length
- [[ft_strcspn]] - Length of segment with NO chars from s2

## Wiki Links
03_Exams/Level_2_INDEX|Level 2 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 72 lines)
