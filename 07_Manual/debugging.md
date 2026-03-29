---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# Debugging

---
tags:
  - [Manual, gray]
---

> ~={blue} Finding and fixing bugs =~

## Navigation
← [[C11_Index|Vault Home]]

## lldb (Debugger)
```bash
# Compile with debug info
cc -g -Wall -Wextra -Werror file.c

# Start debugger
lldb ./a.out

# Commands
b main          # Breakpoint at main
r               # Run
n               # Next line
s               # Step into
p variable      # Print variable
bt              # Backtrace
q               # Quit
```

## valgrind (Memory Checker)
```bash
# Check for memory leaks
valgrind --leak-check=full ./a.out

# Check for invalid access
valgrind --tool=memcheck ./a.out
```

## Common Errors
| Error | Cause |
|-------|-------|
| Segmentation fault | Invalid memory access |
| Bus error | Misaligned access |
| Abort | Double free, corruption |
| Leak | Missing free() |

How do you find memory leaks?
::
`valgrind --leak-check=full ./a.out`

## Related
- 01_Concepts/malloc|malloc/free
- 07_Manual/compilation|Compilation
