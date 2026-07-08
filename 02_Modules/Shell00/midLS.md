---
tags: [Shell00, magenta]
---


# midLS

## What it does
Lists files and directories with comma separation and `/` suffix for directories.

## The Insight
Combines multiple `ls` flags to format output. `-m` adds commas, `-p` adds `/` to directories.

## Step-by-step Algorithm
1. Use `ls` with `-m` for comma separation
2. Add `-p` to mark directories with `/`
3. Combine: `ls -m -p`

## The Code
```bash
ls -m -p
```

## Flag Explanation
| Flag | Effect |
|------|--------|
| `-m` | Comma-separated list |
| `-p` | Add `/` to directory names |



## Line-by-Line Translation
| Line | Code | Translation |
|------|------|-------------|
| 1 | `ls` | Command to list directory contents |
| 2 | `-m` | Fill width with a comma separated list of entries |
| 3 | `-p` | Append a character `/` to directories to distinguish them |

## Common Traps
- ❌ Using `-1` (one per line) which conflicts with `-m`
- ❌ Forgetting `-p` and missing directory markers
- ❌ Hidden files appearing unexpectedly

## Related Concepts
- ls_flags
- file_types

## Propedeuticity
**Prerequisites:** Basic shell navigation
**Unlocks:** More complex ls combinations


---
← [[Shell00_Index|Back to Shell00 Index]]
