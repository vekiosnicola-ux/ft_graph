---
tags: [Level_2, exam]
Level: 2
Topic: String Manipulation
Exercise: snake_to_camel
---


# snake_to_camel

## What It Does
Converts snake_case to camelCase. Removes '_' and uppercases the following letter.

## The Insight
When you see '_', skip it and uppercase the next character by subtracting 32. The character after '_' should have 32 subtracted to convert lowercase to uppercase.

## Step-by-Step Algorithm
1. Count length (subtract number of underscores from original)
2. `malloc(len+1)`
3. Iterate: if '_' skip it and uppercase next char (subtract 32)
4. Else copy normally

## Code
```c
int i = 0, j = 0;                                 // i=source index, j=dest index
int camel_len = 0;                                // Length counter for camelCase result

// First pass: calculate length (underscores are removed)
while (str[i])                                    // Loop through source string
{
    if (str[i] != '_')                            // If character is not underscore
        camel_len++;                               // Count as one character
    i++;                                          // Move to next source character
}

char *camel = malloc(camel_len + 1);               // Allocate result string (+1 for null terminator)
i = 0;                                             // Reset source index to 0

// Second pass: build camelCase string
while (j < camel_len)                             // Loop through destination positions
{
    if (str[i] == '_')                            // If underscore in source
    {
        i++;                                       // Skip the underscore character
        camel[j] = str[i] - 32;                   // Uppercase next char (subtract 32 in ASCII)
    }
    else                                           // Normal character (not underscore)
        camel[j] = str[i];                         // Copy character as-is
    j++;                                          // Move to next dest position
    i++;                                          // Move to next source character
}
camel[camel_len] = '\0';                         // Null-terminate the result string
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int i = 0, j = 0;` | Declare source (i) and dest (j) indices |
| `int camel_len = 0;` | Initialize length counter for camelCase result |
| `while (str[i])` | First pass: calculate length |
| `{` | Start of first while body |
| `if (str[i] != '_')` | If character is not underscore |
| `camel_len++;` | Increment length counter |
| `i++;` | Move to next source character |
| `}` | End of first while body |
| `char *camel = malloc(camel_len + 1);` | Allocate memory for result string |
| `i = 0;` | Reset source index to 0 |
| `while (j < camel_len)` | Second pass: build camelCase string |
| `{` | Start of second while body |
| `if (str[i] == '_')` | If current source char is underscore |
| `{` | Start of underscore handling |
| `i++;` | Skip the underscore |
| `camel[j] = str[i] - 32;` | Uppercase the character after underscore |
| `}` | End of underscore handling |
| `else` | Normal character (not underscore) |
| `camel[j] = str[i];` | Copy character as-is |
| `j++;` | Move dest index forward |
| `i++;` | Move source index forward |
| `}` | End of second while body |
| `camel[camel_len] = '\0';` | Add null terminator to result |

## Common Traps
- ❌ Going out of bounds if string ends with '_' (next char doesn't exist)
- ❌ Not uppercasing after underscore (forgetting to subtract 32)
- ❌ Forgetting null terminator
- ❌ Forgetting to skip the underscore before processing next char

## Related Exercises
- [[camel_to_snake]] - Reverse operation
- [[ft_strcapitalize]] - Capitalize first letter of each word

## Wiki Links
03_Exams/Level_2_INDEX|Level 2 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 81 lines)
