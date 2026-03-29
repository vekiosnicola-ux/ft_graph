---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# <ctype.h> Functions

---
tags:
  - [Manual, gray]
---

> ~={blue} Character classification =~

## Navigation
← [[C11_Index|Vault Home]]

## ⚠️ NOT ALLOWED IN 42
You must reimplement these functions!

## Functions
| Function | Description | ASCII Range |
|----------|-------------|-------------|
| `isalpha(c)` | Is letter | A-Z, a-z |
| `isdigit(c)` | Is digit | 0-9 |
| `isalnum(c)` | Is alphanumeric | A-Z, a-z, 0-9 |
| `isascii(c)` | Is ASCII | 0-127 |
| `isprint(c)` | Is printable | 32-126 |
| `toupper(c)` | To uppercase | a-z → A-Z |
| `tolower(c)` | To lowercase | A-Z → a-z |

What is the ASCII difference between cases?
::
32. Uppercase + 32 = Lowercase

## Related
- C04/INDEX|C04 Utilities
- 01_Concepts/ascii_math|ASCII Math
