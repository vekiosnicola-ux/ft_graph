---
tags: []
date: 2026-03-29
status: complete
---
# ASCII Math

---
tags: [Concepts, blue]
---

## The Insight

Characters in C are just numbers. The ASCII table assigns each printable character a value 0-127. This means you can do math on characters.

## ASCII Table Reference

| Characters | ASCII Range | Example |
|------------|------------|---------|
| Control chars | 0-31 | None printable |
| Digits | 48-57 | '0' = 48 |
| Uppercase | 65-90 | 'A' = 65 |
| Lowercase | 97-122 | 'a' = 97 |

## The Magic Number: 32

Uppercase and lowercase letters differ by exactly 32:

```c
'A' + 32 = 'a'  // 65 + 32 = 97
'a' - 32 = 'A'  // 97 - 32 = 65
```

## Uppercase ↔ Lowercase

From C02 ex07 `ft_strupcase`:

```c
char *ft_strupcase(char *str)
{
    int i = 0;
    while (str[i] != '\0')
    {
        if (str[i] >= 'a' && str[i] <= 'z')
            str[i] = str[i] - 32;  // Subtract 32 to uppercase
        i++;
    }
    return str;
}
```

From C02 ex08 `ft_strlowcase`:

```c
char *ft_strlowcase(char *str)
{
    int i = 0;
    while (str[i] != '\0')
    {
        if (str[i] >= 'A' && str[i] <= 'Z')
            str[i] = str[i] + 32;  // Add 32 to lowercase
        i++;
    }
    return str;
}
```

## Digit to Number

From C02 ex03 `ft_str_is_numeric`:

```c
// To check if character is a digit:
if (str[i] >= '0' && str[i] <= '9')
```

From the textbook `ft_atoi`:

```c
// To convert digit character to integer value:
int digit = str[i] - '0';  // '5' - '0' = 5
```

This works because digits are consecutive in ASCII.

## Combining: Number to Digit

```c
// To convert integer 0-9 to character:
char c = digit + '0';  // 5 + '0' = '5'
```

## rot_13: Alphabet Math

From textbook Level 1 exercise:

```c
// Rotate by 13 positions in alphabet
if (c >= 'a' && c <= 'z')
    c = 'a' + (c - 'a' + 13) % 26;
if (c >= 'A' && c <= 'A')
    c = 'A' + (c - 'A' + 13) % 26;
```

## Checking Character Types Without Library Functions

42 forbids `<ctype.h>` functions like `isupper()`, `isdigit()`, etc. Do it manually:

```c
int ft_str_is_alpha(char *str)
{
    int i = 0;
    while (str[i] != '\0')
    {
        // Not A-Z and not a-z
        if (!((str[i] >= 'A' && str[i] <= 'Z') || 
              (str[i] >= 'a' && str[i] <= 'z')))
            return 0;
        i++;
    }
    return 1;
}
```

## Converting to Hex Nibble

From C02 ex12 `ft_print_memory`:

```c
// Convert byte (0-15) to hex character
char *hex = "0123456789abcdef";
char high = hex[c / 16];   // High nibble
char low = hex[c % 16];    // Low nibble
```

## Why This Matters

ASCII math enables:
- Case conversion without library functions
- Digit character detection and conversion
- Character classification (alpha, digit, printable)
- Rot13 and similar ciphers

## Key Takeaway

Characters are integers. The ASCII values form sequences you can exploit:
- Consecutive ranges for checking (`'0'` to `'9'`)
- 32 difference between uppercase and lowercase
- Alphabet wraparound for rotation (modulo 26)

---

**Related:** [[invisible_skeleton]], [[write_syscall]], [[null_terminator]]
