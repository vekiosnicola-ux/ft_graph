---
tags: [Level_2, exam]
Level: 2
Topic: Bit Manipulation
Exercise: swap_bits
---


# swap_bits

## What It Does
Swaps the high nibble (bits 4-7) with the low nibble (bits 0-3) of a byte.

## The Insight
Simple bitwise math. Shift high nibble right by 4 to move it to low position, shift low nibble left by 4 to move it to high position, OR them together.

## Step-by-Step Algorithm
`return ((byte >> 4) | (byte << 4));`

## Code
```c
unsigned char swap_bits(unsigned char octet)    // Function: takes byte, returns byte with swapped nibbles
{
    return ((octet >> 4) | (octet << 4));       // Shift high nibble right 4, low nibble left 4, OR together
}
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `unsigned char swap_bits(unsigned char octet)` | Define function: takes byte, returns byte |
| `{` | Start of function body |
| `return ((octet >> 4) | (octet << 4));` | High nibble right shift 4 (to low), low nibble left shift 4 (to high), OR combine |
| `}` | End of function |

## Common Traps
- ❌ Forgetting parentheses around shift expressions (operator precedence)
- ❌ Using wrong shift directions (must be opposite for each nibble)
- ❌ Not ORing the two shift results together
- ❌ Forgetting this is a one-liner function (no intermediate variables needed)

## Related Exercises
- [[print_bits]] - Binary output
- [[reverse_bits]] - Bit reversal

## Wiki Links
03_Exams/Level_2_INDEX|Level 2 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 59 lines)
