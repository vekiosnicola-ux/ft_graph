---
tags: [Shell00, magenta]
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



## Line-by-Line Translation
| Line | Code | Translation |
|------|------|-------------|
| 1 | `echo "Z"` | Prints the string "Z" to the standard output, followed by a newline |
| 2 | `>` | Output redirection operator: sends the standard output into a file instead of the terminal |
| 3 | `z` | The target file where the output will be written |

## Common Traps
- ❌ Using `echo -n` would output without newline
- ❌ Forgetting the quotes around Z

## Related Concepts
- shell_redirection

## Propedeuticity
**Prerequisites:** None (first Shell00 exercise)
**Unlocks:** More complex file/shell operations


---
← [[Shell00_Index|Back to Shell00 Index]]
