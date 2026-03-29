---
tags: [Concepts]
---


# Read and Write System Calls

## What It Is
`read()` and `write()` are low-level system calls that transfer data between user space and kernel space (or files/devices). Unlike `fread`/`fwrite` (buffered I/O), these are direct system calls that interact with the operating system kernel for every operation.

## Key Points
- `read(fd, buffer, count)`: reads up to `count` bytes FROM fd INTO buffer, returns bytes read (0=EOF, -1=error)
- `write(fd, buffer, count)`: writes `count` bytes FROM buffer TO fd, returns bytes written (-1=error)
- Buffer must be valid memory, count should be size_t, fd is valid file descriptor
- `write(1, &c, 1)` outputs one character to stdout (fd=1)
- Low-level means no buffering; each call is a kernel transition

## Related Concepts
- file_descriptors
- write_system_call
- buffered_io

## Examples
```c
 <unistd.h>

// Write a single character
void ft_putchar(char c) {
    write(1, &c, 1);
}

// Write a string
void ft_putstr(const char *str) {
    int i = 0;
    while (str[i] != '\0') {
        write(1, &str[i], 1);
        i++;
    }
}

// Read one character from stdin
int ft_getchar(void) {
    char c;
    if (read(0, &c, 1) == 1)
        return c;
    return -1;
}

// Read entire file into buffer (up to n bytes)
ssize_t read_file(const char *filename, char *buf, size_t n) {
    int fd = open(filename, O_RDONLY);
    if (fd == -1)
        return -1;
    ssize_t bytes_read = read(fd, buf, n);
    close(fd);
    return bytes_read;
}

// Write with error checking
int safe_write(int fd, const void *buf, size_t count) {
    size_t written = 0;
    while (written < count) {
        ssize_t result = write(fd, buf + written, count - written);
        if (result == -1)
            return -1;  // error
        written += result;
    }
    return 0;  // success
}
```

## Common Mistakes
- ❌ Passing wrong number of bytes to write (e.g., `write(1, c, 1)` where c is char, should be `&c`)
- ❌ Not checking return values for errors
- ❌ Assuming read fills the buffer (it may return fewer bytes than requested)
- ❌ Confusing direction: read goes INTO buffer, write comes FROM buffer
