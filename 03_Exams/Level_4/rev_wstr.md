---
tags: [Level_4, exam]
  - string
  - manipulation
  - white
---


# rev_wstr

## What it does
Reverses words in a string. "Hello World" -> "World Hello"

## The Insight
Walk to end, then walk backwards reading words and printing them.

## Step-by-step Algorithm
1. Find end
2. Walk backwards: skip spaces, find word end, find word start, print word, print space
3. Handle no trailing space on last word

## The Code
```c
// rev_wstr: Reverses words in a string
// Example: "Hello World" -> "World Hello"
// Handles: tabs as word separators, no trailing space on last word

void rev_wstr(char *str)
{
    int i = 0, start, end, len = 0;        // i=current index, start=word start, end=word end
    
    // Find length
    while (str[len])                        // Loop until null terminator
        len++;                              // Count characters
    i = len - 1;                           // Start from last character
    
    int first = 1;                         // Flag: first word printed (no leading space)
    
    while (i >= 0)                         // Walk backwards through string
    {
        // Skip spaces
        while (i >= 0 && (str[i] == ' ' || str[i] == '\t'))  // Skip whitespace going backward
            i--;                            // Move left
        
        if (i < 0)                          // If we went past the beginning
            break;                          // Done printing all words
        
        end = i;                            // Mark end of current word (current position)
        
        // Find word start
        while (i >= 0 && str[i] != ' ' && str[i] != '\t')  // Go back until whitespace
            i--;                            // Continue moving left
        
        start = i + 1;                      // Word starts one position after whitespace
        
        // Print word
        if (!first)                         // If not the first word
            write(1, " ", 1);              // Print space before word
        first = 0;                         // Mark first word as printed
        
        while (start <= end)                // Print from start to end of word
        {
            write(1, &str[start], 1);      // Write character
            start++;                        // Move to next character
        }
    }
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 20 | `void rev_wstr(char *str)` | Takes string, prints words in reverse order |
| 22 | `int i = 0, start, end, len = 0;` | i=current position, start=word start, end=word end, len=string length |
| 24-25 | `while (str[len]) len++;` | Find string length by counting to null terminator |
| 26 | `i = len - 1;` | Start from last character (index len-1) |
| 27 | `int first = 1;` | Flag: first word (no space before it) |
| 28-49 | `while (i >= 0)` | Main backwards loop: while not past beginning of string |
| 30-31 | `while (i >= 0 && ...)` | Skip whitespace characters going backwards |
| 33-34 | `if (i < 0) break;` | If we went past string start, we're done |
| 35 | `end = i;` | Mark where current word ends (at current non-space char) |
| 37-38 | `while (i >= 0 && ...)` | Continue backwards until we hit whitespace or string start |
| 39 | `start = i + 1;` | Word starts one position after we stopped (whitespace or 0) |
| 41-42 | `if (!first) write(1, " ", 1);` | Print space before word (except first word printed) |
| 43 | `first = 0;` | Mark that first word has been printed |
| 44-48 | `while (start <= end)` | Print all characters from start to end position |

## Common Traps
- ❌ Extra space at end (first flag prevents this for first word, but check loop logic)
- ❌ Not finding word boundaries correctly (start = i + 1 is the key insight)
- ❌ Empty strings (while loop won't execute, nothing printed - correct behavior)

## Related
- [[rostring]] - rotate words
- [[ft_split]] - split string
- EXAMS INDEX|Exam INDEX
