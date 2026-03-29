---
tags: [Shell00]
---


# testShell00

## What it does
Creates a file with read-only permissions (444) and packages it into a tar archive.

## The Insight
Teaches file permissions (chmod) and tar archiving. The permission 444 means read-only for all users.

## Step-by-step Algorithm
1. Create empty file: `touch testShell00`
2. Set permissions to 444: `chmod 444 testShell00`
3. Create tar archive: `tar -cf testShell00.tar testShell00`

## The Code
```bash
touch testShell00
chmod 444 testShell00
tar -cf testShell00.tar testShell00
```

## File Permissions Explained
| Permission | Owner | Group | Others |
|------------|-------|-------|--------|
| `444` | read | read | read |
| `r--r--r--` | r | r | r |

## Common Traps
- ❌ Using wrong permission number (e.g., 777)
- ❌ Forgetting to add file to tar
- ❌ Using wrong tar flags

## Related Concepts
- file_permissions
- tar_archive

## Propedeuticity
**Prerequisites:** None
**Unlocks:** Understanding file attributes and archives
