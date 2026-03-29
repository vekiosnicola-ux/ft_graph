---
tags: []
date: 2026-03-29
status: complete
---
# ft_display_file

---
tags: [C10, magenta]
---

## What it does
Recreates the `cat` command - displays file contents to stdout. Reads one or more files and outputs their contents.

## The Insight
Uses `open`, `read`, and `write` syscalls to read files and output them byte by byte (or buffer by buffer) until EOF.

## Step-by-step Algorithm
1. Check command-line arguments. If no args, read from stdin.
2. For each file argument:
   - Open file with `open()` (read-only mode).
   - Read chunks with `read()` into a buffer.
   - Write each chunk to stdout with `write()`.
   - Close file with `close()`.
3. Handle errors (file not found, permission denied, etc.).

## The Code
```c
 <unistd.h>   // POSIX read/write/close functions
 <fcntl.h>    // File control: open() flags like O_RDONLY
 <errno.h>    // Error numbers for diagnostics

int main(int argc, char **argv)  // argc = arg count, argv = array of argument strings
{
    int fd;         // File descriptor: integer handle for open file
    int bytes_read; // Number of bytes actually read from file
    char buf[30720]; // Buffer: 30KB array to hold chunk of file data

    if (argc == 1)  // If only program name, no file argument given
    {
        // Read from standard input (file descriptor 0) instead
        while ((bytes_read = read(0, buf, 30720)) > 0)  // While data is being read
            write(1, buf, bytes_read);  // Output buffer to stdout (fd 1)
        return (0);  // Success exit
    }
    int i = 1;  // Start at argv[1]: first actual argument (skip program name)
    while (i < argc)  // Loop through all provided filenames
    {
        fd = open(argv[i], O_RDONLY);  // Open file read-only; returns fd or -1 on error
        if (fd == -1)  // open() returns -1 if file couldn't be opened
        {
            return (1);  // Exit with error code 1
        }
        while ((bytes_read = read(fd, buf, 30720)) > 0)  // Read file until EOF (0)
            write(1, buf, bytes_read);  // Write each chunk to stdout
        close(fd);  // Close file descriptor to free system resource
        i++;  // Move to next file argument
    }
    return (0);  // Success
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 23 | `#include <unistd.h>` | Header for read(), write(), close() system calls |
| 24 | `#include <fcntl.h>` | Header for open() flags like O_RDONLY (read-only) |
| 25 | `#include <errno.h>` | Header for error handling constants |
| 27 | `int main(int argc, char **argv)` | Program entry point; argc=count, argv[]=arguments |
| 29 | `int fd;` | File descriptor variable: small int ID for open file |
| 30 | `int bytes_read;` | Tracks how many bytes were successfully read |
| 31 | `char buf[30720];` | 30KB buffer for holding file chunks during copy |
| 33 | `if (argc == 1)` | True when user runs program with no file arguments |
| 35 | `while ((bytes_read = read(0, buf, 30720)) > 0)` | Read from stdin (fd 0) into buffer; loop while data exists |
| 36 | `write(1, buf, bytes_read);` | Output the buffer contents to stdout (fd 1) |
| 39 | `int i = 1;` | Initialize index to skip argv[0] (program's own name) |
| 40 | `while (i < argc)` | Loop through each file argument |
| 42 | `fd = open(argv[i], O_RDONLY);` | Open the i-th file read-only; returns fd or -1 on failure |
| 43 | `if (fd == -1)` | Check if open() failed |
| 45 | `return (1);` | Exit with error code 1 |
| 47 | `while ((bytes_read = read(fd, buf, 30720)) > 0)` | Read chunks until end-of-file (0) |
| 48 | `write(1, buf, bytes_read);` | Write each chunk to standard output |
| 49 | `close(fd);` | Close the file descriptor to release system resources |
| 50 | `i++;` | Move to next file in argument list |
| 52 | `return (0);` | Normal program termination |

## Common Traps
- Forgetting to close file descriptors (leak).
- Not handling missing arguments (read from stdin instead).
- Not handling errors from `open` and `read`.
- Using wrong buffer size.

## Related Concepts
- 01_Concepts/fileDescriptors|File Descriptors
- 01_Concepts/read_write_syscalls|read()/write() syscalls
