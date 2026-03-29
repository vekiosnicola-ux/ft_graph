---
tags: [Shell00]
---


# clean

## What it does
Single command that finds and deletes all temporary files (ending with `~` or starting/ending with `#`).

## The Insight
Uses `find` with OR (`-o`) to match multiple filename patterns, combined with `-delete` for safe removal.

## Step-by-step Algorithm
1. Use `find .` to search current directory
2. Add `-type f` for files only
3. Use `\( -name '*~' -o -name '#*#' \)` for OR pattern matching
4. Add `-print -delete`

## The Code
```bash
find . -type f \( -name '*~' -o -name '#*#' \) -print -delete
```

## Command Breakdown
```bash
find .                           # Start from current directory
  -type f                       # Only files (not directories)
  \( -name '*~' -o -name '#*#' \)  # OR: ends with ~ OR starts/ends with #
  -print                        # Show found files
  -delete                       # Delete found files
```

## Pattern Breakdown
| Pattern | Matches | Example |
|---------|---------|---------|
| `*~` | Ends with tilde | `file.txt~`, `main.c~` |
| `#*#` | Starts & ends with # | `#file#`, `##temp##` |

## Common Traps
- ❌ Forgetting parentheses `\( \)` for proper grouping
- ❌ Putting `-delete` before `-print`
- ❌ Missing `-type f` and accidentally affecting directories

## Related Concepts
- find_command
- filename_patterns

## Propedeuticity
**Prerequisites:** Basic shell navigation
**Unlocks:** Complex file operations with find
