---
tags: [Shell01]
---


# find_sh

## What it does
Finds all shell scripts in current directory and subdirectories, removes `.sh` extension, and sorts results.

## The Insight
Chains `find` with `sed` and `sort` to transform file paths into clean names.

## The Code
```bash
#!/bin/sh
find . -type f -name '*.sh' | sed 's/\.sh$//' | sort
```

## Command Breakdown
| Command | Purpose |
|---------|---------|
| `find . -type f -name '*.sh'` | Find all .sh files |
| `sed 's/\.sh$//'` | Remove .sh extension |
| `sort` | Alphabetical sorting |

## Common Traps
- ❌ Not escaping the dot in regex
- ❌ Forgetting `$` to anchor to end
- ❌ Using `-name` instead of `-type f`

## Related Concepts
- find_command
- sed_regex

## Propedeuticity
**Prerequisites:** Shell00, basic find usage
**Unlocks:** Complex file searching
