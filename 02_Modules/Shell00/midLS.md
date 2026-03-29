---
tags: [Shell00]
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
