---
tags: [Concepts]
---


# Digit Extraction

## What It Is
Digit extraction is the process of separating individual digits from a number. Uses integer division (`/`) to remove digits from the right and modulo (`%`) to get the rightmost digit. Fundamental for problems like `ft_putnbr`, `print_bits`, and converting between bases.

## Key Points
- `n % 10` gives the last digit (rightmost)
- `n / 10` removes the last digit
- Process repeatedly to extract all digits (typically with recursion for printing)
- Order matters: to print digits left-to-right, recurse before printing
- Works for any base: `n % base`, `n / base`

## Related Concepts
- [[division_modulo]]
- [[modulo_division]]
- [[ft_putnbr]]

## Examples
```c
// Get last digit
int last_digit = n % 10;

// Get all digits and print them (right-to-left)
void print_digits(int n) {
    if (n < 0) {
        write(1, "-", 1);
        n = -n;
    }
    if (n >= 10)
        print_digits(n / 10);  // recurse first for left-to-right
    write(1, &(char){'0' + n % 10}, 1);
}

// Count digits in a number
int count_digits(int n) {
    int count = 0;
    if (n == 0) return 1;
    if (n < 0) n = -n;
    while (n > 0) {
        count++;
        n /= 10;
    }
    return count;
}

// Extract digits into array (reversed order)
int *digits_to_array(int n, int *size) {
    if (n == 0) {
        *size = 1;
        int *result = malloc(sizeof(int));
        result[0] = 0;
        return result;
    }
    int temp = n;
    *size = 0;
    if (temp < 0) temp = -temp;
    while (temp > 0) {
        (*size)++;
        temp /= 10;
    }
    int *result = malloc((*size) * sizeof(int));
    for (int i = 0; i < *size; i++) {
        result[i] = n % 10;
        n /= 10;
    }
    return result;
}
```

## Common Mistakes
- ❌ Forgetting to handle negative numbers before division/modulo
- ❌ Printing digits without recursion (would print right-to-left instead of left-to-right)
- ❌ Not handling n = 0 case specially
