---
tags: [Level_3, exam]
  - whitespace-handling
  - white
Level: 3
Topic: String Manipulation
Exercise: expand_str
---


# expand_str

## What It Does
Same as epur_str but separates words with EXACTLY 3 spaces (instead of 1).

## The Insight
Identical logic to epur_str, just print 3 spaces instead of 1 when transitioning between words.

## Step-by-Step Algorithm
Same as epur_str, change `write(1," ",1)` to `write(1,"   ",3)`.

## Code
```c
int flag = 0;                                   // Flag: 0=not after space, 1=after space
int i = 0;                                      // String index

while (av[1][i] == ' ' || av[1][i] == '\t')   // Skip leading spaces/tabs
    i++;

while (av[1][i])                               // Loop through entire string
{
    if (av[1][i] == ' ' || av[1][i] == '\t')  // If current char is space or tab
        flag = 1;                               // Set flag (we just saw whitespace)
    if (!(av[1][i] == ' ' || av[1][i] == '\t')) // If current char is NOT whitespace (is a letter)
    {
        if (flag)                               // If flag is set (we just finished a word)
            write(1, "   ", 3);                // Write exactly 3 spaces (key difference from epur_str)
        flag = 0;                               // Reset flag
        write(1, &av[1][i], 1);               // Write the character
    }
    i++;                                         // Move to next character
}

write(1, "\n", 1);                             // Print final newline
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int flag = 0;` | Initialize flag to 0 (not after space) |
| `int i = 0;` | Initialize string index to 0 |
| `while (av[1][i] == ' '\|\| av[1][i] == '\t')` | Skip leading spaces/tabs |
| `i++;` | Move past leading whitespace |
| `while (av[1][i])` | Loop through entire string |
| `{` | Start of while body |
| `if (av[1][i] == ' '\|\| av[1][i] == '\t')` | If current char is whitespace |
| `flag = 1;` | Set flag to 1 (just saw whitespace) |
| `if (!(av[1][i] == ' '\|\| av[1][i] == '\t'))` | If current char is NOT whitespace (is letter) |
| `{` | Start of letter handling |
| `if (flag)` | If flag is set (we just finished a word) |
| `write(1, "   ", 3);` | Write exactly 3 spaces |
| `flag = 0;` | Reset flag to 0 |
| `write(1, &av[1][i], 1);` | Write the character |
| `}` | End of letter handling |
| `i++;` | Move to next character |
| `}` | End of while body |
| `write(1, "\n", 1);` | Print final newline |

## Common Traps
- ❌ Same as epur_str but writing wrong number of spaces (must be exactly 3)
- ❌ Forgetting exactly 3 spaces between words
- ❌ Printing trailing space at end
- ❌ Not skipping leading spaces

## Related Exercises
- [[epur_str]] - Same but with 1 space between words

## Wiki Links
03_Exams/Level_3_INDEX|Level 3 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 46 lines)
