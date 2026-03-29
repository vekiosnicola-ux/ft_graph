---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# Moulinette

---
tags:
  - [Manual, gray]
---

> ~={red} The automated grader =~

## Navigation
← [[C11_Index|Vault Home]]

## What is it?
Automated testing system that evaluates your code.

## How it works
1. Compiles with `cc -Wall -Wextra -Werror`
2. Runs norminette check
3. Executes test cases
4. Checks output matches expected
5. Tests edge cases

## Common Failures
- ❌ Compilation errors
- ❌ Norminette violations
- ❌ Wrong output format
- ❌ Missing edge cases (NULL, empty string, INT_MIN)
- ❌ Memory leaks

## Tips
- Test with empty strings
- Test with NULL pointers
- Test with INT_MIN/INT_MAX
- Check trailing newlines
- Verify exact output format

What does moulinette check?
::
1. Compilation (no warnings)
2. Norminette (coding style)
3. Output correctness
4. Edge cases

## Related
- 07_Manual/norminette|Norminette
- 07_Manual/compilation|Compilation
