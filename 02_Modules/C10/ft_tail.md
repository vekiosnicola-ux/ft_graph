---
tags: []
date: 2026-03-29
status: complete
---
# ft_tail

---
tags: [C10, magenta]
---

## Navigation
← C10_INDEX|C10 INDEX | [[ft_hexdump|Next: ft_hexdump →]]

## What it does
Recreates the `tail` command - displays the last N lines (default 10) of a file.

## The Insight
To find the last N lines efficiently, read through the file and maintain a circular buffer of the last N line positions.

## Step-by-step Algorithm
1. Parse `-n N` option to get line count (default 10).
2. Open file and get file size.
3. Create circular buffer storing positions of last N newlines.
4. Read file backwards or use lseek to find start of last N lines.
5. Output from that position to end.

## The Code
```c
 <unistd.h>   // POSIX read/write/close/lseek functions
 <fcntl.h>    // File control: open() flags
 <stdlib.h>   // Standard library: malloc, free, atoi

// Convert string of digits to integer (simple atoi implementation)
int ft_atoi(char *str)  // "123" -> 123
{
    int n = 0;  // Accumulator for the numeric result
    while (*str >= '0' && *str <= '9')  // While current char is a digit
    {
        n = n * 10 + (*str - '0');  // Build number: shift left (×10) and add new digit
        str++;  // Move to next character in string
    }
    return (n);  // Return the computed integer
}

int main(int argc, char **argv)  // Program entry point
{
    int fd;         // File descriptor for opened file
    int bytes_read; // Count of bytes read in each read() call
    char buf[30720]; // 30KB buffer for reading file contents
    int n = 10;    // Default: show last 10 lines
    int start = 1; // Index of first file argument (0=program, 1=first file)

    // Parse -n N option: ./ft_tail -n 5 file.txt
    if (argc > 1 && argv[1][0] == '-' && argv[1][1] == 'n')  // Check for -n flag
    {
        n = ft_atoi(argv[2]);  // Convert string "5" to integer 5
        start = 3;  // Files start at argv[3] (skip program, -n, and N)
    }
    // If no file provided, read from stdin
    if (argc <= start)  // User ran program with no file arguments
    {
        while ((bytes_read = read(0, buf, 30720)) > 0)  // Read stdin
            write(1, buf, bytes_read);  // Write to stdout
        return (0);  // Done
    }
    int i = start;  // Point to first actual file argument
    while (i < argc)  // Process each file argument
    {
        fd = open(argv[i], O_RDONLY);  // Open file read-only
        if (fd == -1)  // Error opening file
        {
            i++;  // Skip to next file
            continue;  // Move to next iteration
        }
        // Count total bytes in file by reading byte-by-byte
        bytes_read = 0;
        while (read(fd, buf, 1) > 0)  // Read 1 byte at a time to count
            bytes_read++;  // Increment counter
        lseek(fd, -1, SEEK_END);  // Position file pointer at last byte (1 before EOF)
        int lines = 0;  // Counter for newlines found
        int pos = bytes_read - 1;  // Start from last byte position
        // Count backwards to find the Nth-to-last newline
        while (pos >= 0 && lines < n)  // Walk backwards until we find N newlines
        {
            if (buf[pos] == '\n')  // If current byte is a newline character
                lines++;  // We've found another newline
            if (lines < n)  // Only decrement if we still need more newlines
                pos--;  // Move to previous byte
        }
        lseek(fd, pos + 1, SEEK_SET);  // Position at first byte of last N lines
        while ((bytes_read = read(fd, buf, 30720)) > 0)  // Read and output remaining lines
            write(1, buf, bytes_read);  // Print to stdout
        close(fd);  // Close file descriptor
        i++;  // Move to next file
    }
    return (0);  // Success
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 25 | `int ft_atoi(char *str)` | Convert character string to integer |
| 27 | `int n = 0;` | Accumulator starts at zero |
| 28 | `while (*str >= '0' && *str <= '9')` | Loop while current character is digit 0-9 |
| 30 | `n = n * 10 + (*str - '0');` | Build number: previous digits shift left, add new digit |
| 36 | `int main(int argc, char **argv)` | Program entry point |
| 41 | `int n = 10;` | Default number of lines to display |
| 44 | `if (argc > 1 && argv[1][0] == '-' && argv[1][1] == 'n')` | Check if first arg is -n flag |
| 46 | `n = ft_atoi(argv[2]);` | Parse the number from "5" to 5 |
| 47 | `start = 3;` | First file is at argv[3] (after program, -n, N) |
| 51 | `while ((bytes_read = read(0, buf, 30720)) > 0)` | Read from stdin until EOF |
| 64 | `fd = open(argv[i], O_RDONLY);` | Open file in read-only mode |
| 69-70 | (byte counting loop) | Read every byte to count total file size |
| 71 | `lseek(fd, -1, SEEK_END);` | Position pointer at last byte |
| 74 | `while (pos >= 0 && lines < n)` | Walk backwards counting newlines |
| 77 | `lseek(fd, pos + 1, SEEK_SET);` | Position at start of last N lines |
| 79-80 | (output loop) | Read remaining lines and print them |

## Common Traps
- Forgetting to handle `-n` option.
- Not handling file smaller than N lines.
- Using lseek incorrectly (off-by-one errors).
- Not resetting position for each file.
