---
tags: [Level_3, exam]
  - word-capitalization
  - white
Level: 3
Topic: String Manipulation
Exercise: rstr_capitalizer
---


# rstr_capitalizer

## What It Does
Capitalizes the LAST letter of every word, lowercases everything else. Words counted from the END.

## The Insight
Capitalize when current char is a letter AND next char is space/tab/null. Else lowercase. We look ahead instead of behind.

## Step-by-Step Algorithm
1. Iterate `i` through string
2. If `isalpha(str[i])` AND `isalpha(str[i+1])` is false (next is space/end), uppercase `str[i]`
3. Else if `isalpha`, lowercase `str[i]`
4. Else write unchanged

## Code
```c
int i = 0;                                       // String index, starting at 0

while (str[i])                                   // Loop until null terminator
{
    // Check if current character is a letter
    if ((str[i] >= 'a' && str[i] <= 'z') || (str[i] >= 'A' && str[i] <= 'Z'))
    {
        // If next char is space, tab, or null: this is end of word, uppercase it
        if (str[i + 1] == ' ' || str[i + 1] == '\t' || str[i + 1] == '\0')
            write(1, &(str[i] - 32), 1);        // Uppercase: subtract 32 from ASCII
        else                                      // Inside word: lowercase it
            write(1, &(str[i] + 32), 1);        // Lowercase: add 32 to ASCII
    }
    else                                          // Non-letter character
        write(1, &str[i], 1);                    // Write unchanged
    i++;                                           // Move to next character
}
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int i = 0;` | Initialize string index to 0 |
| `while (str[i])` | Loop until null terminator |
| `{` | Start of while body |
| `if ((str[i] >= 'a' && str[i] <= 'z') \|\| (str[i] >= 'A' && str[i] <= 'Z'))` | Check if current char is a letter |
| `{` | Start of letter handling block |
| `if (str[i + 1] == ' ' \|\| str[i + 1] == '\t' \|\| str[i + 1] == '\0')` | Check if next char is space, tab, or null (end of word) |
| `write(1, &(str[i] - 32), 1);` | Uppercase: subtract 32 from ASCII |
| `else` | Inside a word (not at end) |
| `write(1, &(str[i] + 32), 1);` | Lowercase: add 32 to ASCII |
| `}` | End of letter handling block |
| `else` | Non-letter character |
| `write(1, &str[i], 1);` | Write unchanged |
| `i++;` | Move to next character |
| `}` | End of while body |

## Common Traps
- ❌ Checking wrong condition for end-of-word (checking previous char instead of next)
- ❌ Not lowercasing non-end letters within words
- ❌ Accessing `str[i+1]` at end of string (safe because '\0' is readable and handled)
- ❌ Forgetting that '\0' (null terminator) is readable in this context

## Related Exercises
- [[str_capitalizer]] - Capitalizes FIRST letter of every word
- [[ft_strcapitalize]] - Capitalize first letter of each word

## Wiki Links
03_Exams/Level_3_INDEX|Level 3 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 51 lines)
