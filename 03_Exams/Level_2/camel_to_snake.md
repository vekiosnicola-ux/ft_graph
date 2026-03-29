---
tags: [Level_2, exam]
Level: 2
Topic: String Manipulation
Exercise: camel_to_snake
---


# camel_to_snake

## What It Does
Converts camelCase to snake_case. Inserts '_' before each uppercase letter and lowercases it.

## The Insight
First calculate the length needed (each uppercase letter adds 1 extra char for underscore). Then iterate and insert '_' + lowercase before each uppercase char.

## Step-by-Step Algorithm
1. Count length needed (add 1 for underscore before each uppercase, except first char)
2. `malloc(len+1)`
3. Iterate: if uppercase AND not first char, add '_' before
4. Add lowercase version (`char + 32` in ASCII)
5. Else copy normally

## Code
```c
int i = 0, j = 0;                                 // i=source index, j=dest index
int snake_len = 0;                                // Length counter for snake_case result

// First pass: calculate length needed
while (str[i])                                   // Loop through source string
{
    if (str[i] >= 'A' && str[i] <= 'Z' && i != 0)  // If uppercase letter and not first char
        snake_len++;                               // Add 1 extra for underscore
    snake_len++;                                  // Add 1 for the character itself
    i++;                                          // Move to next source character
}

char *snake = malloc(snake_len + 1);             // Allocate result string (+1 for null terminator)
i = 0;                                            // Reset source index to 0

// Second pass: build snake_case string
while (j <= snake_len)                            // Loop through destination positions
{
    if (str[i] >= 'A' && str[i] <= 'Z')           // If current char is uppercase letter
    {
        if (i != 0)                               // If not first character of string
            snake[j++] = '_';                     // Insert underscore before uppercase
        snake[j] = str[i] + 32;                   // Convert uppercase to lowercase (add 32 in ASCII)
    }
    else                                           // Normal character (already lowercase)
        snake[j] = str[i];                         // Copy character as-is
    j++;                                          // Move dest index forward
    i++;                                          // Move source index forward
}
snake[snake_len] = '\0';                         // Null-terminate the result string
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `int i = 0, j = 0;` | Declare source (i) and dest (j) indices |
| `int snake_len = 0;` | Initialize length counter for snake_case result |
| `while (str[i])` | First pass: calculate length needed |
| `{` | Start of first while body |
| `if (str[i] >= 'A' && str[i] <= 'Z' && i != 0)` | If uppercase and not at start |
| `snake_len++;` | Add 1 extra for underscore |
| `snake_len++;` | Add 1 for the character itself |
| `i++;` | Move to next source character |
| `}` | End of first while body |
| `char *snake = malloc(snake_len + 1);` | Allocate memory for result string |
| `i = 0;` | Reset source index to 0 |
| `while (j <= snake_len)` | Second pass: build snake_case string |
| `{` | Start of second while body |
| `if (str[i] >= 'A' && str[i] <= 'Z')` | If current char is uppercase |
| `{` | Start of uppercase handling |
| `if (i != 0)` | If not first character of string |
| `snake[j++] = '_';` | Insert underscore before uppercase |
| `snake[j] = str[i] + 32;` | Convert uppercase to lowercase |
| `}` | End of uppercase handling |
| `else` | Normal character (lowercase) |
| `snake[j] = str[i];` | Copy character as-is |
| `j++;` | Move dest index forward |
| `i++;` | Move source index forward |
| `}` | End of second while body |
| `snake[snake_len] = '\0';` | Add null terminator to result |

## Common Traps
- ❌ Placing underscore before first letter (must check `i!=0`)
- ❌ Not adding 32 to convert uppercase to lowercase
- ❌ Forgetting null terminator
- ❌ Forgetting second pass resets i to 0

## Related Exercises
- [[snake_to_camel]] - Reverse operation
- [[ft_strcapitalize]] - Capitalize first letter of each word

## Wiki Links
03_Exams/Level_2_INDEX|Level 2 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 84 lines)
