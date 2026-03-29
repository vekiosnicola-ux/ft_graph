---
tags: [Level_2, exam]
Level: 2
Topic: Bit Manipulation
Exercise: print_bits
---


# print_bits

## What It Does
Takes a byte (unsigned char) and prints its binary representation (8 bits), from bit 7 (leftmost) to bit 0 (rightmost).

## The Insight
Bitwise shift and mask. For each bit position 7 down to 0: shift right by `i`, AND with 1 to isolate the bit value, write '1' or '0'.

## Step-by-Step Algorithm
1. Iterate `i` from 7 down to 0
2. For each `i`: `bit = (byte >> i) & 1`
3. Write '0' or '1' based on bit value
4. Return byte unchanged

## Code
```c
unsigned char print_bits(unsigned char byte)     // Function: takes byte, returns byte (unchanged)
{
    int i = 7;                                  // Start from bit 7 (leftmost/high-order bit)

    while (i >= 0)                              // Loop from 7 down to 0
    {
        // Shift bit to position 0, AND with 1 to isolate it, write "1" or "0"
        write(1, (byte >> i) & 1 ? "1" : "0", 1);
        i--;                                     // Move to next bit (rightward)
    }

    return byte;                                // Return byte unchanged (as per spec)
}
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `unsigned char print_bits(unsigned char byte)` | Define function: takes byte, returns byte unchanged |
| `{` | Start of function body |
| `int i = 7;` | Start with bit position 7 (leftmost/highest bit) |
| `while (i >= 0)` | Loop while bit position >= 0 (8 iterations total) |
| `{` | Start of while body |
| `write(1, (byte >> i) & 1 ? "1" : "0", 1);` | Shift right by i, AND with 1, write "1" or "0" |
| `i--;` | Decrement bit position to move rightward |
| `}` | End of while loop |
| `return byte;` | Return byte unchanged |
| `}` | End of function |

## Common Traps
- ❌ Iterating 0 to 7 instead of 7 to 0 (produces reversed output)
- ❌ Using bitwise OR instead of AND
- ❌ Confusing shift direction (left vs right)
- ❌ Not using unsigned char (signed char causes implementation-defined behavior)

## Related Exercises
- [[swap_bits]] - Nibble swapping within a byte
- [[reverse_bits]] - Bit reversal

## Wiki Links
03_Exams/Level_2_INDEX|Level 2 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 67 lines)
