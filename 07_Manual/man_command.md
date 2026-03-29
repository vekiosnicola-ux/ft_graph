---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# How to Use `man`

---
tags:
  - [Manual, gray]
---

> ~={blue} The most important exam tool =~

## Navigation
← [[C11_Index|Vault Home]]

## What is `man`?
The manual page system. Shows documentation for commands, functions, and files.

## Syntax
```bash
man [section] command/function
```

## Sections
| Section | Content |
|---------|---------|
| 1 | User commands |
| 2 | System calls |
| 3 | Library functions |
| 4 | Special files |
| 5 | File formats |
| 6 | Games |
| 7 | Miscellaneous |
| 8 | Admin commands |

## Exam Usage
```bash
# Find write() function
man 2 write

# Find strlen() function
man 3 strlen

# Find printf() function
man 3 printf
```

## Navigation
| Key | Action |
|-----|--------|
| `q` | Quit |
| `/pattern` | Search forward |
| `n` | Next match |
| `N` | Previous match |
| `Space` | Page down |
| `b` | Page up |

How do you find the man page for write()?
::
`man 2 write` - section 2 for system calls

How do you search in man?
::
Press `/` then type pattern, press `n` for next match

## Related
- 07_Manual/linux_commands|Linux Commands
- 07_Manual/c_string.h|C String Functions
