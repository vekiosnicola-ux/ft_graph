---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# <unistd.h> Functions

---
tags:
  - [Manual, gray]
---

> ~={blue} System calls for 42 =~

## Navigation
← [[C11_Index|Vault Home]]

## Key Functions

### write
```c
ssize_t write(int fd, const void *buf, size_t count);
```
- `fd`: 1=stdout, 2=stderr
- `buf`: ADDRESS of data
- `count`: bytes to write

### read
```c
ssize_t read(int fd, void *buf, size_t count);
```
Reads from fd into buf.

### close
```c
int close(int fd);
```
Closes file descriptor.

How do you print a character with write?
::
`write(1, &c, 1)` - pass ADDRESS (&c), not value

## Related
- 01_Concepts/write_syscall|write() Concept
- C00/INDEX|C00
