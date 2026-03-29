---
tags: [Level_2, exam]
Level: 2
Topic: String Manipulation
Exercise: ft_strspn
---


# ft_strspn

## What It Does
Returns the length of the initial segment of s1 that contains ONLY characters from s2. (Opposite of ft_strcspn.)

## The Insight
Count consecutive chars from s1 that ALL exist in s2. Stop at the first char not in s2.

## Step-by-Step Algorithm
1. Iterate `i` through s1
2. For each `s1[i]`, check if it exists in s2
3. If NOT in s2, return `i` (segment ended)
4. Continue if found in s2

## Code
```c
int i = 0, j, found;                              // i=s1 index, j=s2 index, found=match flag

while (s1[i])                                     // Loop through s1 until end
{
    found = 0;                                    // Reset found flag for each character
    j = 0;                                        // Reset s2 index to check from beginning
    while (s2[j])                                 // Loop through s2 to find s1[i]
    {
        if (s1[i] == s2[j])                       // If s1[i] exists in s2
        {
            found = 1;                             // Set found flag to 1 (match found)
            break;                                 // No need to check further in s2
        }
        j++;                                       // Check next char in s2
    }
    if (!found)                                    // If s1[i] was NOT found in s2
        return i;                                  // Return current index (segment ended)
    i++;                                           // Move to next character in s1
}
return i;                                          // Return total length (all chars were valid)
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int i = 0, j, found;` | Declare indices and found flag |
| `while (s1[i])` | Loop through s1 until null terminator |
| `found = 0;` | Reset found flag to 0 for current character |
| `j = 0;` | Reset s2 index to check from start |
| `while (s2[j])` | Loop through s2 looking for s1[i] |
| `if (s1[i] == s2[j])` | Check if s1[i] matches any char in s2 |
| `found = 1;` | Set found flag to 1 (match found) |
| `break;` | Exit s2 loop early (match found) |
| `j++;` | Check next character in s2 |
| `}` | End of s2 while loop |
| `if (!found)` | If s1[i] was not found in s2 |
| `return i;` | Return current index (segment ended) |
| `i++;` | Move to next character in s1 |
| `}` | End of s1 while loop |
| `return i;` | Return total length (all chars were valid) |

## Common Traps
- ❌ Confusing with ft_strcspn (opposite behavior)
- ❌ Not resetting `found=0` for each character (would keep old value)
- ❌ Missing final return when entire s1 is valid
- ❌ Forgetting break when match found (unnecessary s2 checking)

## Related Exercises
- [[ft_strcspn]] - Opposite function (no chars from s2)
- [[ft_strpbrk]] - Returns pointer instead of length
- [[ft_strspn]] - Length of segment with ONLY chars from s2

## Wiki Links
03_Exams/Level_2_INDEX|Level 2 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 75 lines)
