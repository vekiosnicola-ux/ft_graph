---
tags: [Level_3, exam]
  - whitespace-handling
  - white
Level: 3
Topic: String Manipulation
Exercise: epur_str
---


# epur_str

## What It Does
Takes a string, skips leading/trailing spaces, prints words separated by exactly ONE space.

## The Insight
Flag system. Set flag when you see space/tab, only print space when you encounter the NEXT letter (word start), then reset flag.

## Step-by-Step Algorithm
1. Skip leading spaces/tabs
2. `flag = 0`
3. Loop: if space/tab, set `flag=1`. If letter AND flag set, print " ", reset flag, print letter.
4. Else if letter, just print
5. Don't print trailing space

## Code
```c
int flag = 0;                                   // Flag: 0=no space before, 1=space before
int i = 0;                                      // String index

while (av[1][i] == ' ' || av[1][i] == '\t')   // Skip leading spaces and tabs
    i++;

while (av[1][i])                               // Loop through entire string
{
    if (av[1][i] == ' ' || av[1][i] == '\t')  // If current char is space or tab
        flag = 1;                               // Set flag to 1 (saw whitespace)
    if (!(av[1][i] == ' ' || av[1][i] == '\t')) // If current char is NOT whitespace (is a letter)
    {
        if (flag)                               // If flag is set (we just finished a word)
            write(1, " ", 1);                  // Write exactly 1 space before this letter
        flag = 0;                               // Reset flag (no space before next char)
        write(1, &av[1][i], 1);               // Write the letter
    }
    i++;                                         // Move to next character
}

write(1, "\n", 1);                             // Print final newline
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int flag = 0;` | Initialize flag to 0 (no preceding space) |
| `int i = 0;` | Initialize string index to 0 |
| `while (av[1][i] == ' '\|\| av[1][i] == '\t')` | Skip leading spaces and tabs |
| `i++;` | Move past leading whitespace |
| `while (av[1][i])` | Loop through entire string until null terminator |
| `{` | Start of while body |
| `if (av[1][i] == ' '\|\| av[1][i] == '\t')` | If current char is whitespace |
| `flag = 1;` | Set flag to 1 (we just saw whitespace) |
| `if (!(av[1][i] == ' '\|\| av[1][i] == '\t'))` | If current char is NOT whitespace (is a letter) |
| `{` | Start of letter handling block |
| `if (flag)` | If flag is set (we just finished a word) |
| `write(1, " ", 1);` | Write exactly 1 space |
| `flag = 0;` | Reset flag (no space before next char) |
| `write(1, &av[1][i], 1);` | Write the character |
| `}` | End of letter handling block |
| `i++;` | Move to next character |
| `}` | End of while body |
| `write(1, "\n", 1);` | Print final newline |

## Common Traps
- ❌ Printing trailing space at end (the inner if only prints when flag is set and a letter comes)
- ❌ Not skipping leading spaces (would start with space)
- ❌ Using wrong condition in inner if (forgetting the negation)
- ❌ Forgetting to reset flag after printing space
- ❌ Not handling both space and tab as whitespace

## Related Exercises
- [[expand_str]] - Same but with 3 spaces between words
- [[last_word]] - Related word extraction

## Wiki Links
03_Exams/Level_3_INDEX|Level 3 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 50 lines)
