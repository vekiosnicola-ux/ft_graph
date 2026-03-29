---
tags: [Shell00]
---


# ft_magic

## What it does
Creates a "magic" file that detects files containing "42" at byte position 42.

## The Insight
Unix `file` command uses magic numbers/patterns to identify file types. The magic file defines patterns at specific byte offsets.

## Step-by-step Algorithm
1. Create magic file with format: `offset type test message`
2. Use offset `42`, type `string`, test `42`
3. Message: `42 file`
4. Test with: `file -m ft_magic testfile`

## The Magic File (ft_magic)
```
42      string  42      42 file
```

## Format Explanation
| Field | Value | Meaning |
|-------|-------|---------|
| offset | `42` | Look at byte 42 |
| type | `string` | Compare as string |
| test | `42` | Expected value |
| message | `42 file` | Output when matched |

## Common Magic Types
| Type | Meaning |
|------|---------|
| `byte` | 1-byte decimal/octal/hex value |
| `short` | 2-byte value |
| `long` | 4-byte value |
| `string` | Character string |

## Common Traps
- ❌ Off-by-one in offset (byte indexing starts at 0)
- ❌ Wrong tab spacing in magic file
- ❌ Forgetting the message field

## Related Concepts
- file_command
- binary_patterns

## Propedeuticity
**Prerequisites:** Understanding of bytes and file structure
**Unlocks:** File format analysis
