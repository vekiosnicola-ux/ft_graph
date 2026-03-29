---
tags: [Shell01]
---


# count_files

## What it does
Counts the number of files in the current directory and all subdirectories.

## The Insight
Uses `find` to locate all files, then `wc -l` to count lines.

## The Code
```bash
#!/bin/sh
find . -type f | wc -l
```

## Command Breakdown
| Command | Purpose |
|---------|---------|
| `find . -type f` | Find all regular files |
| `wc -l` | Count lines (one file per line) |

## Common Traps
- ❌ Using `-type d` instead of `-type f`
- ❌ Not excluding hidden files properly
- ❌ Counting directories as files

## Related Concepts
- find_command
- wc_command

## Propedeuticity
**Prerequisites:** Shell00
**Unlocks:** File system traversal
