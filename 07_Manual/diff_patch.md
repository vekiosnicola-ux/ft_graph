---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# diff & patch

---
tags:
  - [Manual, gray]
---

> ~={blue} File comparison and patching =~

## Navigation
← [[C11_Index|Vault Home]]

## diff
Compare files line by line.

```bash
diff file1 file2
```

### Output
- No output = files identical
- `< line` = line only in file1
- `> line` = line only in file2

### Options
| Option | Description |
|--------|-------------|
| `-u` | Unified format (preferred) |
| `-c` | Context format |
| `-q` | Quick check (different or not) |

## patch
Apply differences to a file.

```bash
# Create patch
diff -u old.c new.c > fix.patch

# Apply patch
patch old.c < fix.patch
```

How do you check if two files are identical?
::
`diff file1 file2` - no output means identical

## Related
- Shell00/diff|diff Exercise
