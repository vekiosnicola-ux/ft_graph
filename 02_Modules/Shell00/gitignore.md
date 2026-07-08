---
tags: [Shell00, magenta]
---


# gitignore

## What it does
Script that lists all files ignored by the current git repository.

## The Insight
Uses `git ls-files` with `--ignored` flag to see what git is ignoring based on `.gitignore` rules.

## Step-by-step Algorithm
1. Use `git ls-files` with `--ignored` flag
2. Add `--exclude-standard` to apply `.gitignore` rules
3. Output the list

## The Code
```bash
#!/bin/bash
git ls-files --ignored --exclude-standard
```

## Command Breakdown
| Flag | Purpose |
|------|---------|
| `--ignored` | Show only ignored files |
| `--exclude-standard` | Apply rules from `.gitignore` files |

## Common .gitignore Patterns
```bash
*.log          # Ignore all log files
*.tmp          # Ignore temp files
.DS_Store      # Ignore macOS metadata
node_modules/  # Ignore entire directories
```



## Line-by-Line Translation
| Line | Code | Translation |
|------|------|-------------|
| 1 | `#!/bin/bash` | The shebang: tells the OS to execute this script using the `bash` shell |
| 2 | `git ls-files` | Git command to list files in the repository |
| 3 | `--ignored` | Show only ignored files |
| 4 | `--exclude-standard` | Respect the standard ignore rules (e.g., `.gitignore`) |

## Common Traps
- ❌ Using `--others` without understanding its effect
- ❌ Not applying `--exclude-standard` for proper gitignore behavior
- ❌ Expecting untracked-but-not-ignored files

## Related Concepts
- gitignore_rules
- git_ls_files

## Propedeuticity
**Prerequisites:** Git basics
**Unlocks:** Managing git repositories effectively


---
← [[Shell00_Index|Back to Shell00 Index]]
