---
tags: [Level_4, exam]
  - string
  - manipulation
  - white
---


# rostring

## What it does
Moves first word to end of string, prints result with single spaces between words.

## The Insight
Find first word boundaries, skip spaces after it, print rest, print space, print first word.

## Step-by-step Algorithm
1. Skip leading spaces
2. Mark first word start/end
3. Skip spaces after first word
4. Print rest of string (compressing spaces)
5. Print space
6. Print first word

## The Code
```c
// rostring: Rotates words in a string (first word moves to end)
// Example: "  hello   world  foo" -> "world foo hello"
// Handles: multiple spaces, tabs, single word (no rotation)

void rostring(char *str)
{
    int i = 0, start, end, len = 0;        // i=index, start=word start, end=word end
    
    // Skip leading spaces
    while (str[i] == ' ' || str[i] == '\t')  // Skip space or tab
        i++;                                  // Move to next character
    
    start = i;                                // Mark where first word starts
    
    // Find first word end
    while (str[i] && str[i] != ' ' && str[i] != '\t')  // While not end and not whitespace
        i++;                                  // Move to end of first word
    end = i;                                  // Mark where first word ends
    
    // Skip spaces after first word
    while (str[i] == ' ' || str[i] == '\t')  // Skip whitespace after first word
        i++;                                  // Position i at start of "rest" of string
    
    // Print rest of string (compressing spaces)
    int first = 1;                            // Flag: first word being printed (no leading space)
    while (str[i])                            // Loop through rest of string
    {
        if (str[i] != ' ' && str[i] != '\t') // If current char is not whitespace
        {
            if (!first)                       // If not the first word we're printing
                write(1, " ", 1);             // Print space separator
            first = 0;                        // Mark that we've printed at least one word
            while (str[i] && str[i] != ' ' && str[i] != '\t')  // Print entire word
            {
                write(1, &str[i], 1);         // Write current character
                i++;                          // Move to next character
            }
        }
        else                                  // Current char is whitespace
            i++;                              // Skip it (compress multiple spaces)
    }
    
    // Print space and first word
    if (start < end)                          // If there was a first word (string not empty)
    {
        if (!first)                           // If we printed something before
            write(1, " ", 1);                 // Print space before first word
        while (start < end)                   // Print the first word we saved earlier
        {
            write(1, &str[start], 1);         // Write character
            start++;                          // Advance to next character
        }
    }
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 23 | `void rostring(char *str)` | Function takes string, prints rotated version |
| 25 | `int i = 0, start, end, len = 0;` | i=current index, start=first word start, end=first word end |
| 27-28 | `while (str[i] == ' ' \|\| str[i] == '\t') i++;` | Skip leading whitespace |
| 29 | `start = i;` | Save position where first word begins |
| 31-32 | `while (str[i] && str[i] != ' ' && str[i] != '\t') i++;` | Move to first whitespace after word |
| 33 | `end = i;` | Save position where first word ends |
| 35-36 | `while (str[i] == ' ' \|\| str[i] == '\t') i++;` | Skip whitespace after first word |
| 38 | `int first = 1;` | Flag: track if this is first word to avoid leading space |
| 39-54 | `while (str[i])` | Loop through rest of string |
| 41-42 | `if (str[i] != ' ' && str[i] != '\t')` | If current char is part of a word |
| 43-44 | `if (!first) write(1, " ", 1);` | Print space before word (except first) |
| 45 | `first = 0;` | Mark that first word has been printed |
| 46-50 | `while (str[i] && ...)` | Print all chars of current word |
| 53 | `else i++;` | Skip whitespace (this compresses multiple spaces) |
| 56-65 | `if (start < end)` | Print the saved first word at the end |
| 58-59 | `if (!first) write(1, " ", 1);` | Space before first word if needed |
| 60-64 | `while (start < end)` | Print characters from start to end |

## Common Traps
- ❌ Strings with only one word (just print it unchanged - no extra space)
- ❌ Trailing spaces (compressed by the algorithm, handled correctly)
- ❌ Not compressing multiple spaces (would cause extra spaces in output)

## Related
- [[rev_wstr]] - reverse words
- [[ft_split]] - split string
- EXAMS INDEX|Exam INDEX
