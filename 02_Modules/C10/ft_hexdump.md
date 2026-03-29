---
tags: []
date: 2026-03-29
status: complete
---
# ft_hexdump

---
tags: [C10, magenta]
---

## Navigation
← C10_INDEX|C10 INDEX | [[ft_strace|Next: ft_strace →]]

## What it does
Recreates the `hexdump -C` command - displays file contents in hexadecimal and ASCII format.

## The Insight
Each line shows: offset (8 hex digits), 16 hex bytes (2 digits each), and ASCII representation.

## Step-by-step Algorithm
1. Read file in 16-byte chunks.
2. For each chunk:
   - Print offset as 8-digit hex.
   - Print 16 bytes as 2-digit hex (space-separated).
   - Print ASCII representation (printable chars as-is, others as '.').
3. Pad last line if fewer than 16 bytes.

## The Code
```c
 <unistd.h>   // POSIX read/write functions
 <fcntl.h>    // File control: open() flags

// Convert a single byte to its 2-digit hexadecimal representation
void print_hex_byte(unsigned char c)  // Takes byte like 255, prints "ff"
{
    char *hex = "0123456789abcdef";  // Lookup table: index gives hex character
    write(1, &hex[c / 16], 1);       // High nibble (first hex digit): 255/16 = 15 -> 'f'
    write(1, &hex[c % 16], 1);       // Low nibble (second hex digit): 255%16 = 15 -> 'f'
}

// Print 8-digit hexadecimal offset (address)
void print_offset(int offset)  // Prints memory offset like "0000001a"
{
    char *hex = "0123456789abcdef";  // Hex character lookup table
    char buf[8];                      // Buffer to hold 8 hex characters
    int i = 7;                        // Start filling from last position

    while (i >= 0)  // Fill buffer right-to-left with hex digits
    {
        buf[i] = hex[offset % 16];  // Get last hex digit of offset
        offset /= 16;                // Remove last digit for next iteration
        i--;                         // Move left to next position
    }
    write(1, buf, 8);  // Output all 8 hex digits at once
}

int main(int argc, char **argv)  // Program entry point
{
    int fd;                    // File descriptor for open file
    unsigned char buf[16];     // Buffer for exactly 16 bytes
    int bytes_read;            // Count of bytes actually read
    int offset = 0;            // Current position in file (in bytes)
    int i;                     // Loop counter for byte processing

    // If no arguments, read from stdin
    if (argc == 1)  // Running program with no file argument
    {
        while ((bytes_read = read(0, buf, 16)) > 0)  // Read 16-byte chunks from stdin
        {
            print_offset(offset);  // Print current byte offset in hex
            write(1, " ", 1);      // Space separator
            i = 0;
            while (i < 16)  // Process all 16 possible byte slots
            {
                if (i < bytes_read)  // If this slot has actual data
                    print_hex_byte(buf[i]);  // Print byte as 2 hex digits
                else
                    write(1, "  ", 2);  // Pad with 2 spaces for missing byte
                if (i % 2 == 1)  // After every 2 bytes (odd index), add space
                    write(1, " ", 1);  // Extra space between byte pairs
                i++;
            }
            write(1, " |", 2);  // Pipe separator before ASCII display
            i = 0;
            while (i < bytes_read)  // ASCII representation section
            {
                if (buf[i] >= 32 && buf[i] <= 126)  // If printable ASCII (space through tilde)
                    write(1, (char *)&buf[i], 1);  // Print character directly
                else
                    write(1, ".", 1);  // Non-printable: show dot instead
                i++;
            }
            write(1, "|\n", 2);  // Close ASCII column and newline
            offset += bytes_read;  // Advance offset by bytes actually read
        }
        return (0);
    }
    fd = open(argv[1], O_RDONLY);  // Open specified file read-only
    if (fd == -1)  // Error: file couldn't be opened
        return (1);  // Exit with error code
    // Same reading loop as stdin case above...
    while ((bytes_read = read(fd, buf, 16)) > 0)  // Read 16-byte chunks from file
    {
        print_offset(offset);  // Print current byte offset
        write(1, " ", 1);
        i = 0;
        while (i < 16)  // Print hex representation
        {
            if (i < bytes_read)
                print_hex_byte(buf[i]);
            else
                write(1, "  ", 2);
            if (i % 2 == 1)
                write(1, " ", 1);
            i++;
        }
        write(1, " |", 2);  // ASCII column separator
        i = 0;
        while (i < bytes_read)  // Print ASCII representation
        {
            if (buf[i] >= 32 && buf[i] <= 126)
                write(1, (char *)&buf[i], 1);
            else
                write(1, ".", 1);
            i++;
        }
        write(1, "|\n", 2);  // End of line
        offset += bytes_read;  // Update byte offset
    }
    close(fd);  // Clean up: close file descriptor
    return (0);  // Success
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 25 | `void print_hex_byte(...)` | Helper: converts one byte to two hex characters |
| 27 | `char *hex = "012345..."` | Lookup table where index 10 = 'a', 15 = 'f' |
| 28 | `write(1, &hex[c / 16], 1)` | First hex digit = left 4 bits of byte |
| 29 | `write(1, &hex[c % 16], 1)` | Second hex digit = right 4 bits of byte |
| 32 | `void print_offset(int offset)` | Print 8-digit hex address |
| 37 | `while (i >= 0)` | Build 8-digit string from right to left |
| 54 | `if (argc == 1)` | No file argument: read from stdin |
| 62-70 | (hex display loop) | Print 16 slots: hex bytes or spaces |
| 68 | `if (i % 2 == 1)` | Add extra space between byte pairs |
| 75-79 | (ASCII loop) | Print char if printable, '.' if not |
| 86 | `fd = open(argv[1], O_RDONLY)` | Open first argument as file |
| 89-116 | (file reading loop) | Same output format as stdin case |

## Common Traps
- Not padding missing bytes on last line.
- Forgetting spaces between byte pairs.
- Incorrect ASCII representation handling.
- Not printing offset in 8 digits.
