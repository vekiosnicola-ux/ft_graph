---
tags: [Shell00]
---


# git_commit.sh

## What it does
Shell script that displays the hashes of the last 5 git commits.

## The Insight
Uses `git log` with format specifiers to extract only commit hashes. The `%H` format gives full hash.

## Step-by-step Algorithm
1. Create script with shebang: `#!/bin/sh`
2. Use `git log --format=%H` to get hashes
3. Limit to 5: `-n 5`

## The Code
```bash
#!/bin/sh
git log --format=%H -n 5
```

## Command Breakdown
| Part | Meaning |
|------|---------|
| `git log` | Show commit history |
| `--format=%H` | Output only commit hashes (full) |
| `-n 5` | Limit to 5 most recent commits |

## Format Specifiers
| Specifier | Output |
|-----------|--------|
| `%H` | Commit hash (full) |
| `%h` | Commit hash (short) |
| `%an` | Author name |
| `%s` | Subject (commit message) |

## Common Traps
- ❌ Forgetting to make executable (`chmod +x`)
- ❌ Using `%h` instead of `%H` if full hash needed
- ❌ Not running in a git repository

## Related Concepts
- git_log
- [[git_workflow]]

## Propedeuticity
**Prerequisites:** Git basics
**Unlocks:** Scripted git operations
