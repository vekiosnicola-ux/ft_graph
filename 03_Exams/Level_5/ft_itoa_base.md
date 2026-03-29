---
tags: [Level_5, exam]
  - string
  - conversion
  - bases
  - white
---


# ft_itoa_base

## What it does
Converts integer to string in custom base (2-16). Like ft_itoa but with custom base. LEVEL 5 VERSION requires shortest solution.

## The Insight
Count digits by dividing, allocate, fill from right. For negative numbers, only base 10 gets '-'. INT_MIN needs unsigned cast.

## Step-by-step Algorithm
1. Determine sign for base 10 only
2. Count digits
3. malloc
4. Fill from right using % base and / base
5. Add '-' for negative base 10
6. Null terminate

## The Code
```c
// ft_itoa_base: Converts integer to string in given base (2-16)
// Bases 2-16: digits 0-9, A-F for values 10-15
// Example: ft_itoa_base(255, 16) -> "FF"
// Example: ft_itoa_base(-8, 10) -> "-8"
// INT_MIN handled via unsigned cast to prevent overflow

char *ft_itoa_base(int value, int base){
    char *digits="0123456789ABCDEF";       // Digit lookup table for bases 2-16
    char buf[34];                          // Buffer for result (enough for all bases)
    int pos=33;                            // Start filling from end of buffer (rightmost)
    unsigned int uv=value<0&&base==10?-value:value;  // Handle negative: only for base 10
    if(value<0&&base==10)                  // Only base 10 shows negative sign
        buf[--pos]='-';                    // Write '-' at current position, then decrement pos
    while(uv){                             // Convert number to digits (at least one digit)
        buf[--pos]=digits[uv%base];        // Get remainder (last digit), store at current position
        uv/=base;                           // Remove last digit from number
    }
    return strdup(&buf[pos]);              // strdup copies string from pos to null terminator
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 23 | `char *ft_itoa_base(int value, int base)` | Takes integer value and base (2-16), returns new string |
| 24 | `char *digits="0123456789ABCDEF";` | Lookup table: index 0='0', index 15='F' |
| 25 | `char buf[34];` | Buffer large enough for any result (e.g., -2147483648 in base 2 = 32 bits + sign) |
| 26 | `int pos=33;` | pos = current fill position (start at end, fill backwards) |
| 27 | `unsigned int uv=value<0&&base==10?-value:value;` | Handle negative: if negative AND base 10, convert to positive; otherwise keep as-is (for base 2,8,16 negative uses two's complement) |
| 28-29 | `if(value<0&&base==10) buf[--pos]='-';` | Only base 10 shows negative sign (bases 2,8,16 show two's complement form) |
| 30-32 | `while(uv)` | Main conversion loop: while number is non-zero |
| 31 | `buf[--pos]=digits[uv%base];` | Pre-decrement pos, then store digit character for remainder |
| 32 | `uv/=base;` | Remove last digit (remainder) from number |
| 34 | `return strdup(&buf[pos]);` | Duplicate string starting from first used position |

## Common Traps
- ❌ Only base 10 handles negative sign (bases 2,8,16 typically show unsigned representation)
- ❌ INT_MIN overflow (must use unsigned cast: -INT_MIN = INT_MIN in signed, but -INT_MIN as unsigned = positive)
- ❌ Wrong digit lookup (digits[uv%base] - must use modulo result as index)
- ❌ Forgetting null terminator (strdup handles this by copying until '\0')

## Related
- [[ft_itoa]] - decimal conversion
- [[print_memory]] - hex dump
- EXAMS INDEX|Exam INDEX
