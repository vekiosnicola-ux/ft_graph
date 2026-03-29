---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# Linux Commands Reference

---
tags:
  - [Manual, gray]
---

> ~={blue} Essential commands for 42 =~

## Navigation
← [[C11_Index|Vault Home]]

## File Operations
| Command | Description |
|---------|-------------|
| `ls` | List files |
| `ls -la` | List all with details |
| `ls -m -p` | Comma-separated, mark dirs |
| `cp file1 file2` | Copy file |
| `mv file1 file2` | Move/rename |
| `rm file` | Remove file |
| `rm -rf dir` | Remove directory |
| `mkdir dir` | Create directory |
| `touch file` | Create empty file |
| `cat file` | Display file |
| `head -n 5 file` | First 5 lines |
| `tail -n 5 file` | Last 5 lines |
| `wc -l file` | Count lines |
| `diff file1 file2` | Compare files |
| `find . -name "*.c"` | Find files |
| `grep pattern file` | Search in file |

## Permissions
| Command | Description |
|---------|-------------|
| `chmod 444 file` | Read-only for all |
| `chmod 755 file` | rwx for owner, rx for others |
| `chmod +x file` | Make executable |

## Git
| Command | Description |
|---------|-------------|
| `git clone url` | Clone repository |
| `git add .` | Stage all changes |
| `git commit -m "msg"` | Commit changes |
| `git push` | Push to remote |
| `git log --oneline` | Compact log |
| `git status` | Show status |

What does `ls -m -p` do?
::
Comma-separated list with `/` after directories

How do you find all .sh files?
::
`find . -name "*.sh"`

## Related
- 07_Manual/file_permissions|File Permissions
- 07_Manual/git_workflow|Git Workflow
