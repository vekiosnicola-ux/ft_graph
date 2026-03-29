---
tags: [Shell01]
---


# r_dwssap

## What it does
Reverse password swap - reads input, transforms it in a specific way (exact behavior per subject).

## The Insight
Uses `rev` or string reversal techniques. The name "r_dwssap" is "password" reversed!

## The Code
```bash
#!/bin/sh
echo "$1" | rev
```

## Command Breakdown
| Command | Purpose |
|---------|---------|
| `rev` | Reverse characters on each line |

## Common Traps
- ❌ Not handling command line arguments correctly
- ❌ Forgetting to reverse the string back
- ❌ Byte vs character reversal confusion

## Related Concepts
- rev_command
- string_manipulation

## Propedeuticity
**Prerequisites:** Shell01
**Unlocks:** String transformation
