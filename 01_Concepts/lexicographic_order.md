---
tags: [Concepts]
---


# Lexicographic Order

## What It Is
Lexicographic order (dictionary order) arranges strings or sequences based on the order of their elements as they would appear in a dictionary. Characters are compared sequentially from left to right; the first differing character determines the order. Numbers and uppercase/lowercase have specific ordering rules.

## Key Points
- Compare first elements; whichever is smaller determines the order
- If all compared elements are equal, the shorter sequence comes first
- In ASCII: digits (0-9) < uppercase (A-Z) < lowercase (a-z)
- String comparison in C uses `strcmp`, which returns 0 if equal, negative if s1 < s2, positive if s1 > s2
- Character comparison uses ASCII values

## Related Concepts
- [[odometer_algorithm]]
- [[ft_strcmp]]
- [[ft_strcapitalize]]

## Examples
```c
// Lexicographic comparison (like strcmp)
int my_strcmp(const char *s1, const char *s2) {
    while (*s1 && *s1 == *s2) {
        s1++;
        s2++;
    }
    return *s1 - *s2;
}

// Check if string is in lexicographic order
int is_lex_sorted(char **words, int count) {
    for (int i = 0; i < count - 1; i++) {
        if (my_strcmp(words[i], words[i + 1]) > 0)
            return 0;
    }
    return 1;
}

// Examples of lexicographic order:
// "apple" < "banana"     (a < b)
// "abc" < "abcd"         (prefix comes first)
// "ABC" < "abc"          (ASCII: A(65) < a(97))
// "123" < "456"          (ASCII: 1(49) < 4(52))
```

## Common Mistakes
- ❌ Assuming case-insensitive comparison (it's case-sensitive in standard C)
- ❌ Forgetting that shorter strings that are prefixes come first
- ❌ Using `>` or `<` on strings directly instead of `strcmp`
