---
tags: [Level_2, exam]
  - cipher
Level: 2
Topic: String Manipulation
Exercise: alpha_mirror
---


# alpha_mirror

## What It Does
Mirrors the alphabet: a->z, b->y, c->x, etc. Preserves the case of each letter.

## The Insight
The mirror of 'a' is 'z' (they are 25 positions apart in the alphabet). Formula: lowercase: `'z' - (c - 'a')`, uppercase: `'Z' - (c - 'A')`. This reverses the letter's position within its case range.

## Step-by-Step Algorithm
Iterate through each character:
- If uppercase, compute: `new = 'Z' - (c - 'A')`
- If lowercase, compute: `new = 'z' - (c - 'a')`
- Else copy unchanged

## Code
```c
int i = 0;                                         // String index, starting at 0
while (str[i])                                     // Loop until null terminator
{
    char c = str[i];                               // Get current character
    if (c >= 'A' && c <= 'Z')                      // If uppercase letter (A-Z)
        write(1, &('Z' - (c - 'A')), 1);           // Mirror: 'Z' minus offset from 'A'
    else if (c >= 'a' && c <= 'z')                 // If lowercase letter (a-z)
        write(1, &('z' - (c - 'a')), 1);           // Mirror: 'z' minus offset from 'a'
    else                                           // Non-alphabetic character
        write(1, &c, 1);                           // Write unchanged
    i++;                                           // Move to next character
}
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int i = 0;` | Initialize string index to 0 |
| `while (str[i])` | Loop while not at end of string (not '\0') |
| `{` | Start of while body |
| `char c = str[i];` | Store current character in variable c |
| `if (c >= 'A' && c <= 'Z')` | Check if uppercase letter (A-Z range) |
| `write(1, &('Z' - (c - 'A')), 1);` | Compute mirrored uppercase letter and write |
| `else if (c >= 'a' && c <= 'z')` | Check if lowercase letter (a-z range) |
| `write(1, &('z' - (c - 'a')), 1);` | Compute mirrored lowercase letter and write |
| `else` | Non-alphabetic character |
| `write(1, &c, 1);` | Write character unchanged |
| `i++;` | Move to next character |
| `}` | End of while body |

## Common Traps
- ❌ Applying mirror formula to non-alphabetic characters
- ❌ Using wrong formula (mixing up the offset calculation)
- ❌ Not preserving case (mirroring 'A' to 'z' instead of 'Z')
- ❌ Forgetting to write non-alphabetic characters unchanged

## Related Exercises
- [[rot_13]] - Similar character transformation cipher
- [[ulstr]] - Case inversion (not mirroring)
- [[alpha_mirror]] - Alphabet mirroring

## Wiki Links
03_Exams/Level_2_INDEX|Level 2 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 71 lines)
