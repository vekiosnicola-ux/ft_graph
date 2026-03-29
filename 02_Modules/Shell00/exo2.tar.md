---
tags: [Shell00]
---


# exo2.tar

## What it does
This is a tar archive file that needs to be extracted and examined. It contains hidden files that are part of the evaluation.

## The Insight
Learning to work with tar archives - extracting, listing contents, and understanding archive formats.

## Step-by-step Algorithm
1. List contents without extracting: `tar -tf exo2.tar`
2. Extract files: `tar -xf exo2.tar`
3. View hidden files: `ls -la`

## The Code
```bash
# List archive contents
tar -tf exo2.tar

# Extract archive
tar -xf exo2.tar
```

## Common Tar Flags
| Flag | Purpose |
|------|---------|
| `-c` | Create archive |
| `-x` | Extract archive |
| `-t` | List contents |
| `-f` | Specify filename |
| `-v` | Verbose output |

## Common Traps
- ❌ Forgetting `-f` flag when creating/extracting
- ❌ Not checking what's inside before extracting
- ❌ Overwriting existing files without warning

## Related Concepts
- file_permissions
- archive_formats

## Propedeuticity
**Prerequisites:** Basic shell navigation
**Unlocks:** Working with compressed archives
