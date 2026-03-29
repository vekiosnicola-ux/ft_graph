---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# Compilation

---
tags:
  - [Manual, gray]
---

> ~={blue} How to compile for 42 =~

## Navigation
← [[C11_Index|Vault Home]]

## Standard Compilation
```bash
cc -Wall -Wextra -Werror file.c
```

## Flags
| Flag | Meaning |
|------|---------|
| `-Wall` | All warnings |
| `-Wextra` | Extra warnings |
| `-Werror` | Warnings = errors |
| `-o name` | Output filename |
| `-c` | Compile only (no link) |
| `-g` | Debug info |

## Creating Library
```bash
# Compile to object files
cc -Wall -Wextra -Werror -c ft_putchar.c
cc -Wall -Wextra -Werror -c ft_strlen.c

# Create static library
ar rcs libft.a ft_putchar.o ft_strlen.o

# Use library
cc main.c -L. -lft
```

What flags are required for 42?
::
`-Wall -Wextra -Werror`

## Related
- C09/INDEX|C09 Makefile
- 07_Manual/norminette|Norminette
