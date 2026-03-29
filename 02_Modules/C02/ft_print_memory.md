---
tags: [C02, flashcard]
---


# ft_print_memory

## What it does
Prints memory dump: address, 16 hex bytes per line, ASCII representation.

## The Insight
16-byte chunks. Recursive address printing. Hex conversion with lookup table.

## Step-by-step Algorithm
1. Cast addr to unsigned char*
2. Loop i from 0 to size in steps of 16:
   a. Print address as hex
   b. Print 16 hex bytes (space-separated)
   c. Print ASCII representation

## The Code (with pedagogical comments)
```c
void print_hex_byte(unsigned char c)  // Helper: prints one byte as two hex digits
{
    char *hex = "012345abcdef";  // Hex lookup table
    write(1, &hex[c / 16], 1);  // High nibble as hex character
    write(1, &hex[c % 16], 1);  // Low nibble as hex character
}

void print_addr(unsigned long addr)  // Helper: prints address in hex (recursive)
{
    char *hex = "012345abcdef";  // Hex lookup table
    if (addr >= 16)  // If address has more than one digit
        print_addr(addr / 16);  // Recursively print higher digits first
    write(1, &hex[addr % 16], 1);  // Print lowest hex digit
}

void *ft_print_memory(const void *addr, unsigned int size)  // Main function
{
    unsigned char *p = (unsigned char *)addr;  // Cast address to byte pointer
    unsigned int i, j;  // Loop counters (i = line, j = byte within line)

    i = 0;
    while (i < size)  // Process one 16-byte line at a time
    {
        print_addr((unsigned long)(p + i));  // Print memory address as hex
        write(1, " ", 1);  // Print space separator
        j = 0;
        while (j < 16)  // Print 16 hex bytes per line
        {
            if (i + j < size)  // If byte exists
            {
                print_hex_byte(p[i + j]);  // Print byte as two hex digits
                write(1, " ", 1);  // Print space separator
            }
            else
                write(1, "   ", 3);  // If no byte, print three spaces
            j++;
        }
        write(1, " ", 1);  // Print space before ASCII column
        j = 0;
        while (j < 16 && i + j < size)  // Print ASCII representation
        {
            if (p[i + j] >= 32 && p[i + j] <= 126)  // If printable
                write(1, &p[i + j], 1);  // Print the character
            else
                write(1, ".", 1);  // If not printable, print dot
            j++;
        }
        write(1, "\n", 1);  // Print newline to end the line
        i += 16;  // Move to next 16-byte chunk
    }
    return ((void *)addr);  // Return the original address (as required)
}
```

## Line-by-Line Translation
1. `void print_hex_byte(unsigned char c)` - Helper function to print one byte as two hex digits
2. `char *hex = "012345abcdef"` - Lookup table for hex characters
3. `write(1, &hex[c / 16], 1)` - Extract high nibble (divide by 16) and write as hex
4. `write(1, &hex[c % 16], 1)` - Extract low nibble (modulo 16) and write as hex
5. `void print_addr(unsigned long addr)` - Helper function to print memory address recursively
6. `if (addr >= 16)` - If address has multiple hex digits
7. `print_addr(addr / 16)` - Recursively print higher-order digits first
8. `write(1, &hex[addr % 16], 1)` - Print the lowest hex digit
9. `unsigned char *p = (unsigned char *)addr` - Cast the address to a byte pointer
10. `while (i < size)` - Loop through memory in 16-byte chunks
11. `print_addr((unsigned long)(p + i))` - Print the current memory address
12. `while (j < 16)` - Print 16 hex bytes per line
13. `if (i + j < size)` - If this byte exists in the data
14. `print_hex_byte(p[i + j])` - Print the byte as two hex digits
15. `else write(1, "   ", 3)` - If no byte, print spaces to align
16. `while (j < 16 && i + j < size)` - Print ASCII representation column
17. `if (p[i + j] >= 32 && p[i + j] <= 126)` - If byte is printable ASCII
18. `write(1, &p[i + j], 1)` - Print the character
19. `else write(1, ".", 1)` - If not printable, print a dot
20. `return ((void *)addr)` - Return the original address as required

## Common Traps
- ❌ Using printf/sprintf (not allowed)
- ❌ Not padding missing bytes with spaces
- ❌ Not returning addr
- ❌ Off-by-one in hex conversion

## Related Concepts
- 01_Concepts/hex_conversion|Hex Conversion
- 01_Concepts/recursion|Recursion
- [[ft_putstr_non_printable]]

## Related Exercises
- [[ft_putstr_non_printable]]

## Propedeuticity
**Prerequisites:** [[ft_putstr_non_printable]]
**Unlocks:** Exam-level debugging

What does a memory dump show?
::
Each line shows: memory address, 16 hex bytes (space-separated), and ASCII representation (printable chars or dots).
