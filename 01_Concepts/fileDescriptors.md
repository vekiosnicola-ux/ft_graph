---
tags: [Concepts]
---


# File Descriptors

## What It Is
A file descriptor is a non-negative integer that the kernel uses to identify an open file for a process. When you open a file, the kernel returns a small integer (0, 1, 2, 3...) that you use for subsequent operations. Standard file descriptors exist at program start: 0 (stdin), 1 (stdout), 2 (stderr).

## Key Points
- File descriptors are integers: 0=stdin, 1=stdout, 2=stderr
- `open()` returns new file descriptor, `close()` releases it
- `read()` reads data FROM file INTO buffer, `write()` writes FROM buffer TO file
- Each process has its own file descriptor table
- File descriptors can point to files, pipes, sockets, devices
- Always close files when done to avoid resource leaks

## Related Concepts
- [[read_write_syscalls]]
- file_operations
- open_close

## Examples
```c
 <fcntl.h>   // open
 <unistd.h>  // read, write, close

// Open file (read-only)
int fd = open("file.txt", O_RDONLY);
if (fd == -1) {
    // handle error
}

// Read from file into buffer
char buffer[1024];
ssize_t bytes_read = read(fd, buffer, sizeof(buffer));
if (bytes_read == -1) {
    // handle error
}

// Write to file from buffer
const char *msg = "Hello, world!";
ssize_t bytes_written = write(fd, msg, 13);

// Close file descriptor
close(fd);

// Open with flags
int fd_create = open("newfile.txt", O_WRONLY | O_CREAT | O_TRUNC, 0644);
int fd_append = open("log.txt", O_WRONLY | O_CREAT | O_APPEND, 0644);

// File descriptor table:
// 0 = stdin  (read from terminal)
// 1 = stdout (write to terminal)  
// 2 = stderr (write to terminal error)
// 3+ = user-opened files
```

## Common Mistakes
- ❌ Forgetting to close file descriptors (resource leak)
- ❌ Not checking return value of open (returns -1 on error)
- ❌ Confusing read/write direction: read(FROM file TO buffer), write(FROM buffer TO file)
- ❌ Using wrong flags for open (O_RDONLY vs O_WRONLY vs O_RDWR)
