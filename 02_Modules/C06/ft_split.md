---
tags: [C06]
---


# ft_split

## What it Does
Splits a string into an array of words, using `charset` as the delimiter characters.

## The Insight
First pass counts words, then allocate array, then fill with substrings.

## Step-by-step Algorithm
1. If `str` is NULL, return NULL.
2. Count words: iterate through `str`, incrementing count when a non-delimiter is found followed by delimiter or end.
3. Allocate `malloc((count + 1) * sizeof(char *))`.
4. Iterate again, extracting each word as a substring.
5. Set the last element to NULL.
6. Return the array.

## The Code
```c
 <stdlib.h> // Provides malloc() for dynamic memory allocation

// Helper function: checks if character c is in the charset (delimiter)
int ft_is_sep(char c, char *charset)
{
    int i;              // Loop counter to iterate through charset

    i = 0;              // Start at the first character of charset
    while (charset[i])  // Loop through each character until null terminator
    {
        if (c == charset[i])  // Does c match this delimiter?
            return (1);        // Yes: c is a separator/delimiter
        i++;                  // No: check the next character in charset
    }
    return (0);               // c is NOT in charset (not a separator)
}

// Helper function: counts how many words are in the string
int ft_count_words(char *str, char *charset)
{
    int count;          // Counter for number of words found
    int i;              // Index through the input string

    count = 0;          // Start with zero words
    i = 0;              // Start at the beginning of the string
    while (str[i])      // Loop until we hit the null terminator '\0'
    {
        while (str[i] && ft_is_sep(str[i], charset))  // Skip leading separators
            i++;                                       // Move to next character
        if (str[i] && !ft_is_sep(str[i], charset))   // Found start of a word?
        {
            count++;                                   // Yes: increment word counter
            while (str[i] && !ft_is_sep(str[i], charset))  // Skip the entire word
                i++;                                   // Move past all characters of word
        }
    }
    return (count);     // Return total number of words found
}

// Helper function: extracts one word starting at position *pos
char *ft_extract_word(char *str, char *charset, int *pos)
{
    char *word;         // Pointer to the newly allocated word
    int start;          // Starting index of the word in str
    int len;            // Length of the word
    int i;              // Loop counter for copying

    while (str[*pos] && ft_is_sep(str[*pos], charset))  // Skip leading separators
        (*pos)++;                                        // Move to start of word
    start = *pos;                                        // Record where word begins
    while (str[*pos] && !ft_is_sep(str[*pos], charset)) // Find end of word
        (*pos)++;                                        // Move past the word
    len = *pos - start;                                  // Calculate word length
    word = malloc(len + 1);                              // Allocate memory for word
    if (!word)                                           // Check for malloc failure
        return (NULL);                                   // Propagate error
    i = 0;                                               // Copy characters one by one
    while (i < len)                                      // Copy exactly 'len' characters
    {
        word[i] = str[start + i];                        // Copy from source to word
        i++;                                             // Move to next character
    }
    word[i] = '\0';                                      // Null-terminate the word
    return (word);                                       // Return the extracted word
}

// Main function: splits string into array of words
char **ft_split(char *str, char *charset)
{
    char **result;      // Pointer to array of strings (will be returned)
    int count;          // Number of words
    int i;              // Loop counter for filling result array
    int pos;            // Current position in str during extraction

    if (!str)           // Guard: check if input string is NULL
        return (NULL);  // Cannot split a NULL string
    count = ft_count_words(str, charset);                // First pass: count words
    result = malloc((count + 1) * sizeof(char *));       // Allocate array of pointers
    if (!result)        // Check for malloc failure
        return (NULL);  // Propagate error
    pos = 0;            // Start at the beginning of the string
    i = 0;              // Start at first element of result array
    while (i < count)   // Extract each word into result array
    {
        result[i] = ft_extract_word(str, charset, &pos); // Get next word
        i++;                // Move to next position in result array
    }
    result[i] = NULL;    // NULL-terminate the array of strings
    return (result);     // Return the completed array
}
```

## Line-by-Line Translation
- `include <stdlib.h>` — Header for malloc() and free()
- `int ft_is_sep(char c, char *charset)` — Check if c is a delimiter
- `while (charset[i])` — Loop through all delimiters
- `if (c == charset[i]) return (1);` — Found a match: c is a separator
- `return (0);` — No match found: c is not a separator
- `int ft_count_words(char *str, char *charset)` — Count total words in string
- `while (str[i])` — Loop through entire string
- `while (str[i] && ft_is_sep(...)) i++;` — Skip separator characters
- `if (str[i] && !ft_is_sep(...))` — Found start of a word?
- `count++;` — Increment word counter
- `char *ft_extract_word(...)` — Extract one word from string
- `while (str[*pos] && ft_is_sep(...)) (*pos)++;` — Skip leading separators
- `start = *pos;` — Mark where word begins
- `len = *pos - start;` — Calculate length
- `word = malloc(len + 1);` — Allocate memory for the word
- `while (i < len) word[i] = str[start + i];` — Copy characters
- `word[i] = '\0';` — Null-terminate
- `char **ft_split(char *str, char *charset)` — Main splitting function
- `if (!str) return (NULL);` — Handle NULL input
- `count = ft_count_words(str, charset);` — First pass: count words
- `result = malloc((count + 1) * sizeof(char *));` — Allocate array of pointers
- `while (i < count)` — Loop to extract each word
- `result[i] = ft_extract_word(...);` — Fill array with words
- `result[i] = NULL;` — NULL-terminate the array (sentinel value)
- `return (result);` — Return the completed string array

## Related
- ex04 ft_strtrim
- ex03 ft_strjoin
