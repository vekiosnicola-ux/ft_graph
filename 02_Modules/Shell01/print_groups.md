---
tags: [Shell01]
---


# print_groups

## What it does
Prints the groups (secondary groups) of the current user, separated by commas.

## The Insight
Uses `id -nG` to get group names, then `tr` to replace spaces with commas.

## The Code
```bash
#!/bin/sh
id -nG "$FT_USER" | tr ' ' ','
```

## Command Breakdown
| Command | Purpose |
|---------|---------|
| `id -nG` | Print all group names for user |
| `tr ' ' ','` | Replace spaces with commas |

## Common Traps
- ❌ Forgetting the `-n` flag (would print numeric GIDs)
- ❌ Not quoting `$FT_USER` (would break on spaces)
- ❌ Using `,` instead of `', '` (needs comma-space)

## Related Concepts
- user_groups
- tr_command

## Propedeuticity
**Prerequisites:** Shell00
**Unlocks:** User management understanding
