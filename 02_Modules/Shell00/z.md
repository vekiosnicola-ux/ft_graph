---
tags: [Shell00]
---


# z

## What it does
Creates a file named `z` that outputs "Z" followed by a newline.

## The Insight
The simplest possible shell exercise. Uses basic output redirection with `echo`.

## Step-by-step Algorithm
1. Use `echo` to print "Z" (adds newline by default)
2. Redirect output to file `z` using `>`

## The Code
```bash
echo "Z" > z
```

## Common Traps
- ❌ Using `echo -n` would output without newline
- ❌ Forgetting the quotes around Z

## Related Concepts
- shell_redirection

## Propedeuticity
**Prerequisites:** None (first Shell00 exercise)
**Unlocks:** More complex file/shell operations
