---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# <stdlib.h> Functions

---
tags:
  - [Manual, gray]
---

> ~={blue} Standard library utilities =~

## Navigation
← [[C11_Index|Vault Home]]

## Memory
| Function | Description |
|----------|-------------|
| `malloc(size)` | Allocate memory |
| `free(ptr)` | Free memory |
| `calloc(n, size)` | Allocate zeroed array |
| `realloc(ptr, size)` | Resize allocation |

## Conversion
| Function | Description |
|----------|-------------|
| `atoi(str)` | String to int |
| `atof(str)` | String to float |
| `itoa(n, str, base)` | Int to string |

## Program
| Function | Description |
|----------|-------------|
| `exit(status)` | Exit program |
| `abort()` | Abort program |
| `system(cmd)` | Run shell command |

What does malloc return on failure?
::
NULL - always check!

## Related
- C06/INDEX|C06 Malloc
- 01_Concepts/malloc|malloc Concept
