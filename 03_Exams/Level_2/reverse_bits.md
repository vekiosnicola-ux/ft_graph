---
tags: [Level_2, exam]
Level: 2
Topic: Bit Manipulation
Exercise: reverse_bits
---


# reverse_bits

## What It Does
Reverses all 8 bits of a byte. Bit 0 becomes bit 7, bit 1 becomes bit 6, etc.

## The Insight
Build result byte bit by bit. For each iteration: shift result left to make room, OR in the rightmost bit of original, shift original right to bring next bit into position.

## Step-by-Step Algorithm
1. `result = 0`
2. Loop 8 times: `result <<= 1`, `result |= (byte & 1)`, `byte >>= 1`
3. Return result

## Code
```c
unsigned char reverse_bits(unsigned char byte)  // Function: takes byte, returns reversed byte
{
    unsigned char result = 0;                   // Initialize result accumulator to 0
    int i = 0;                                  // Loop counter for 8 bits

    while (i < 8)                               // Loop exactly 8 times (once per bit)
    {
        result <<= 1;                            // Shift result left by 1 (make room for next bit)
        result |= (byte & 1);                   // OR with rightmost bit of original byte
        byte >>= 1;                             // Shift original right by 1 (next bit becomes rightmost)
        i++;                                     // Increment loop counter
    }

    return result;                              // Return the fully reversed byte
}
```

## Line-by-Line Translation
| Line | Translation |
|------|-------------|
| `unsigned char reverse_bits(unsigned char byte)` | Define function: takes byte, returns reversed byte |
| `{` | Start of function body |
| `unsigned char result = 0;` | Initialize result accumulator to 0 |
| `int i = 0;` | Initialize loop counter to 0 |
| `while (i < 8)` | Loop exactly 8 times (for 8 bits) |
| `{` | Start of while body |
| `result <<= 1;` | Shift result left by 1 bit (make room for next bit) |
| `result \|= (byte & 1);` | OR with rightmost bit of original byte |
| `byte >>= 1;` | Shift original right by 1 (next bit becomes rightmost) |
| `i++;` | Increment loop counter |
| `}` | End of while loop |
| `return result;` | Return the fully reversed byte |
| `}` | End of function |

## Common Traps
- ❌ Not using unsigned char (signed causes implementation-defined overflow)
- ❌ Wrong loop count (must be exactly 8)
- ❌ Forgetting to shift byte each iteration (would always read same bit)
- ❌ Forgetting to shift result left (bits would overwrite)

## Related Exercises
- [[print_bits]] - Binary output
- [[swap_bits]] - Nibble swapping within a byte

## Wiki Links
03_Exams/Level_2_INDEX|Level 2 INDEX | EXAMS INDEX|Exams INDEX

(End of file - total 69 lines)
