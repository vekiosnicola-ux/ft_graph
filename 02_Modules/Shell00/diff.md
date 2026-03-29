---
tags: [Shell00]
---


# diff

## What it does
Creates a file identical to another file, such that `diff a b` produces no output.

## The Insight
The `diff` command compares files line-by-line. If identical, it outputs nothing. Using `cp` creates an exact copy.

## Step-by-step Algorithm
1. Use `cp` to copy file `a` to file `b`
2. Verify with `diff a b` (should produce no output)
3. Optional: redirect to empty file with `diff a b > sw.diff`

## The Code
```bash
cp a b
```

## The diff Command
```bash
diff [options] file1 file2

Output:
  (no output)  : files are identical
  > line      : line exists only in file2
  < line      : line exists only in file1
```

## Common Traps
- ❌ Using `ln` instead of `cp` (symlinks point to same inode)
- ❌ Not understanding that diff is line-oriented
- ❌ Using `diff` on binary files (produces binary differences)

## Related Concepts
- file_copy
- [[diff_patch]]

## Propedeuticity
**Prerequisites:** Basic file operations
**Unlocks:** Understanding file comparison and patching
