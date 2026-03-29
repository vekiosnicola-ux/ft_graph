---
tags: [Level_3, exam]
  - word-capitalization
  - white
Level: 3
Topic: String Manipulation
Exercise: str_capitalizer
---


# str_capitalizer

## What It Does
Capitalizes the FIRST letter of every word, lowercases everything else.

## The Insight
Capitalize when current char is a letter AND (previous char is space/tab OR i==0). Else lowercase.

## Step-by-Step Algorithm
1. Iterate `i` through string
2. If `isalpha(str[i])` AND (`i==0` OR `str[i-1]==' '` OR `str[i-1]=='\t'`), uppercase
3. Else if `isalpha`, lowercase
4. Else write unchanged

## Code
```c
int i = 0;                                       // String index, starting at 0
while (str[i])                                   // Loop until null terminator
{
    // Check if current character is a letter (uppercase or lowercase)
    if ((str[i] >= 'a' && str[i] <= 'z') || (str[i] >= 'A' && str[i] <= 'Z'))
    {
        // If first char OR preceded by space/tab: uppercase it
        if (i == 0 || str[i - 1] == ' ' || str[i - 1] == '\t')
            write(1, &(str[i] - 32), 1);        // Uppercase: subtract 32 from ASCII value
        else                                      // Inside a word: lowercase it
            write(1, &(str[i] + 32), 1);        // Lowercase: add 32 to ASCII value
    }
    else                                          // Non-letter (space, digit, etc.)
        write(1, &str[i], 1);                    // Write unchanged
    i++;                                           // Move to next character
}
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int i = 0;` | Initialize string index to 0 |
| `while (str[i])` | Loop through each character until null terminator |
| `{` | Start of while body |
| `if ((str[i] >= 'a' && str[i] <= 'z') \|\| (str[i] >= 'A' && str[i] <= 'Z'))` | Check if current char is a letter |
| `{` | Start of letter handling block |
| `if (i == 0 \|\| str[i - 1] == ' ' \|\| str[i - 1] == '\t')` | Check if at word start (first char OR preceded by whitespace) |
| `write(1, &(str[i] - 32), 1);` | Uppercase the letter (subtract 32 from ASCII) |
| `else` | Inside a word (not at start) |
| `write(1, &(str[i] + 32), 1);` | Lowercase the letter (add 32 to ASCII) |
| `}` | End of letter handling block |
| `else` | Non-letter character |
| `write(1, &str[i], 1);` | Write unchanged |
| `i++;` | Move to next character |
| `}` | End of while body |

## Common Traps
- ❌ Accessing `str[i-1]` when `i==0` (must check `i==0` first!)
- ❌ Not lowercasing rest of word (only capitalizing first letter)
- ❌ Using wrong ASCII offset (32 is correct for a<->A conversion)
- ❌ Forgetting to handle both uppercase and lowercase letters

## Related Exercises
- [[rstr_capitalizer]] - Capitalizes LAST letter of every word
- [[ft_strcapitalize]] - Capitalize first letter of each word

## Wiki Links
03_Exams/Level_3_INDEX|Level 3 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 70 lines)
