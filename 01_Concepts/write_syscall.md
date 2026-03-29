---
tags: []
date: 2026-03-29
status: complete
---
# The write() Syscall

---
tags: [Concepts, blue]
---

## What is a System Call?

A system call (syscall) is a request from your program to the operating system's kernel. The `write` syscall outputs data to a file descriptor.

```c
 <unistd.h>

ssize_t write(int fd, const void *buf, size_t count);
```

- `fd`: File descriptor (1 = stdout, 2 = stderr)
- `buf`: **Address** of the data to write
- `count`: Number of bytes to write

## The Critical Mistake: Value vs Address

This is the most common crash cause for 42 students:

```c
char c = 'a';

// ❌ WRONG - passes VALUE (ASCII 97)
write(1, c, 1);
// CPU interprets 97 as an address → reads from illegal address → CRASH

// ✅ CORRECT - passes ADDRESS
write(1, &c, 1);
// CPU reads from valid address of c → SUCCESS
```

The syscall requires an **address** to know WHERE to fetch the data from.

## The ft_putchar Pattern

From C00 ex00 `ft_putchar`:

```c
 <unistd.h>

void ft_putchar(char c)
{
    write(1, &c, 1);
}
```

Simple but essential: `&c` passes the address of the character.

## Writing Multiple Characters

From C00 ex01 `ft_print_alphabet`:

```c
void ft_print_alphabet(void)
{
    char letter = 'a';
    while (letter <= 'z')
    {
        write(1, &letter, 1);  // Need & on each iteration
        letter++;
    }
}
```

Each `write` outputs exactly one byte.

## Why No printf?

In 42 exercises, `printf` is forbidden. This forces you to understand:
1. How data actually flows to the terminal
2. The difference between formatted output and raw bytes
3. The concept of file descriptors

```c
// ❌ Not allowed in 42 exams
printf("Hello");

// ✅ Correct approach
write(1, "Hello", 5);
```

## Understanding File Descriptors

| FD | Meaning |
|----|---------|
| 0 | Standard Input (stdin) |
| 1 | Standard Output (stdout) |
| 2 | Standard Error (stderr) |

```c
write(1, "Hello", 5);  // To stdout
write(2, "Error!", 6);  // To stderr
```

## Writing Strings

```c
write(1, "ABC", 3);  // Writes three bytes: 'A', 'B', 'C'
```

Note: No null terminator needed when specifying count.

## Common Patterns in 42

From C02 ex11 `ft_putstr_non_printable`:

```c
void ft_putchar(char c)
{
    write(1, &c, 1);
}

// Using it in a loop:
while (str[i] != '\0')
{
    write(1, &str[i], 1);
    i++;
}
```

## The Abstraction Barrier

`printf` hides the syscall. `write` reveals it. Understanding `write` means understanding that:
- Everything is a file descriptor
- Data is just bytes at addresses
- The kernel mediates all I/O

## Key Takeaway

The `write` syscall is the foundation of output in C. It requires addresses, not values. This single requirement reveals the entire memory model of the system—data lives at addresses, and syscalls read from those addresses.

---

**Related:** [[pointers]], [[null_terminator]], [[ascii_math]]
