---
tags: [Level_2, exam]
Level: 2
Topic: String Manipulation
Exercise: last_word
---


# last_word

## What It Does
Displays the last word of a string (last sequence of non-space/non-tab characters). Always prints newline.

## The Insight
Walk to end of string, then walk backwards skipping trailing spaces/tabs, find the start of the last word, print it.

## Step-by-Step Algorithm
1. Walk to end: `while(str[i]) i++;`
2. Walk backwards: `while(i>0 && (str[i-1]==' '||str[i-1]=='\t')) i--;`
3. Mark word end, walk forward to find length
4. Write the word using start pointer and length
5. Print newline

## Code
```c
int i = 0;                                       // Initialize string index to 0

while (av[1][i]) i++;                            // Walk forward to end of string (find length)

while (i > 0 && (av[1][i - 1] == ' ' || av[1][i - 1] == '\t'))  // Skip trailing spaces/tabs backwards
    i--;

int start = i;                                   // Record start position of the last word

while (av[1][i] && av[1][i] != ' ' && av[1][i] != '\t')  // Walk forward through the word
    i++;

write(1, &av[1][start], i - start);              // Write the last word: start address and byte count
write(1, "\n", 1);                              // Print final newline
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int i = 0;` | Initialize string index to 0 |
| `while (av[1][i]) i++;` | Move index forward until null terminator (finding string length) |
| `while (i > 0 && (av[1][i-1] == ' '\|\|av[1][i-1] == '\t'))` | Walk backwards, skipping trailing whitespace |
| `i--;` | Decrement i to skip whitespace |
| `int start = i;` | Record the start position of the last word |
| `while (av[1][i] && av[1][i] != ' ' && av[1][i] != '\t')` | Walk forward through the word until whitespace or end |
| `i++;` | Increment i |
| `write(1, &av[1][start], i - start);` | Write the last word: start address and byte count |
| `write(1, "\n", 1);` | Print final newline |

## Common Traps
- ❌ Crashing on empty strings or strings with only spaces
- ❌ Forgetting newline
- ❌ Walking backwards past string start (must check `i > 0`)
- ❌ Not handling multiple trailing spaces/tabs correctly

## Related Exercises
- [[first_word]] - First word extraction (similar logic but forward)
- [[alpha_mirror]] - String character processing

## Wiki Links
03_Exams/Level_2_INDEX|Level 2 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 65 lines)
