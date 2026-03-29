---
tags: []
date: 2026-03-29
status: complete
---
# hello

EXAMS INDEX|Exam INDEX | Level 0

---
tags: [Exams, Level_0, magenta]
---


## What it does
Prints "Hello World!" followed by a newline to standard output.

## Insight
This is the simplest possible exercise - just output a fixed string. The key is knowing that:
1. You must use `write(1, ...)` not `printf`
2. You need to count EXACTLY how many bytes to write (including the newline)
3. The string "Hello World!\n" is 13 bytes: H-e-l-l-o- -W-o-r-l-d-!-\n

This is the foundational exercise that introduces the write() system call.

## Step-by-step Algorithm
1. Write the exact string "Hello World!\n" to file descriptor 1 (stdout)
2. Count the bytes: "Hello World!" = 12 characters, plus '\n' = 13 total bytes
3. Use write(1, "Hello World!\n", 13);

## Code
```c
 <unistd.h>  // Required for write() system call

void hello(void)      // Function takes no arguments, returns nothing
{
    write(1, "Hello World!\n", 13);  // write to stdout (fd=1), 13 bytes
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|-------------|
| 1 | `#include <unistd.h>` | Include the header that provides the `write()` system call |
| 3 | `void hello(void)` | Define a function named `hello` that takes no parameters and returns nothing |
| 4 | `{` | Start of function body |
| 5 | `write(1, "Hello World!\n", 13);` | Write to file descriptor 1 (stdout), the string "Hello World!\n", 13 bytes total |
| 6 | `}` | End of function body |

## Common Traps
- ❌ Miscounting bytes: "Hello World!" is 12 chars, + \n = 13 total
- ❌ Forgetting the newline - output must match exactly
- ❌ Using printf (forbidden in exams)
- ❌ Writing to wrong file descriptor (use 1 for stdout)

## Propedeuticity
None - this is the entry point exercise

## Related Exercises
- [[aff_first_param]] - First exercise using write with strings

(End of file - 48 lines)
