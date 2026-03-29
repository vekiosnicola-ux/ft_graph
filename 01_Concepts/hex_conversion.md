---
tags: [Concepts]
---


# Hexadecimal Conversion

## What It Is
Hexadecimal (base-16) uses digits 0-9 and letters A-F to represent values. It's commonly used in computing because each hex digit represents exactly 4 binary bits (nibble). Converting between decimal, hex, and binary is fundamental for understanding memory addresses, color codes, and low-level data.

## Key Points
- Hex digits: 0-9, A(10), B(11), C(12), D(13), E(14), F(15)
- Prefix `0x` indicates hexadecimal in C (e.g., `0xFF`)
- 4 bits per hex digit: 0xF = 1111 binary = 15 decimal
- Two hex digits = one byte (8 bits): 0xFF = 11111111 binary = 255 decimal
- Conversion: divide by 16 repeatedly to get hex digits (from right to left)

## Related Concepts
- [[digit_extraction]]
- [[ft_putnbr]]
- [[print_bits]]

## Examples
```c
 <unistd.h>

// Convert single digit to hex character
char hex_digit(int n) {
    if (n < 10)
        return '0' + n;
    return 'A' + (n - 10);
}

// Print number in hex (without 0x prefix)
void print_hex(unsigned int n) {
    if (n >= 16)
        print_hex(n / 16);
    write(1, &hex_digit(n % 16), 1);
}

// Print byte as two hex digits
void print_hex_byte(unsigned char c) {
    char *hex = "0123456789abcdef";
    write(1, &hex[c / 16], 1);   // high nibble
    write(1, &hex[c % 16], 1);   // low nibble
}

// Convert hex character to decimal value
int hex_char_to_int(char c) {
    if (c >= '0' && c <= '9')
        return c - '0';
    if (c >= 'A' && c <= 'F')
        return 10 + (c - 'A');
    if (c >= 'a' && c <= 'f')
        return 10 + (c - 'a');
    return -1;  // invalid
}

// Parse hex string to integer
unsigned int parse_hex(const char *hex) {
    unsigned int result = 0;
    int val;
    while ((val = hex_char_to_int(*hex)) >= 0) {
        result = result * 16 + val;
        hex++;
    }
    return result;
}

// Common hex patterns
// 0xFF   = 255    (all bits set in byte)
// 0x0F   = 15     (low nibble set)
// 0xF0   = 240    (high nibble set)
// 0x00   = 0      (all bits clear)
// 0x80   = 128    (MSB set)
// 0x7F   = 127    (MSB clear)
```

## Common Mistakes
- ❌ Forgetting that hex letters can be uppercase or lowercase
- ❌ Confusing hex value with decimal (0xFF = 255, not 15*16=240... wait 15*16+15=255)
- ❌ Not handling hex string with 0x prefix
- ❌ Using wrong conversion for negative numbers
