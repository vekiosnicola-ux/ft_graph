---
tags: []
date: 2026-03-29
status: complete
---
# ft_strace

---
tags: [C10, magenta]
---

## Navigation
← C10_INDEX|C10 INDEX

## What it does
Recreates a simplified `strace` - traces system calls made by a program.

## The Insight
Uses `ptrace` to attach to a process and intercept syscalls. For each syscall, print its name and arguments.

## Step-by-step Algorithm
1. Fork process with `fork()`.
2. In child, use `execvp()` to run the target program.
3. In parent, use `ptrace(PTRACE_SYSCALL, pid, ...)` to step through syscalls.
4. Read syscall number and arguments from registers.
5. Print syscall info and return value.

## The Code
```c
 <unistd.h>      // POSIX API: write, fork, execvp
 <sys/ptrace.h>  // Process tracing: ptrace() function and constants
 <sys/wait.h>    // Wait functions: wait() and status macros
 <sys/syscall.h> // System call numbers: SYS_write, SYS_read, etc.
 <sys/user.h>    // User structure: user_regs_struct for register access

int main(int argc, char **argv)  // Program entry point
{
    int status;                   // Child process exit status from wait()
    long ins;                     // Instruction pointer (not used but required)
    struct user_regs_struct regs; // Structure containing CPU register values

    if (argc < 2)  // Need program name and command to trace
        return (1);  // Exit with error if no command given
    pid_t pid = fork();  // Create a child process copy of this program
    if (pid == 0)  // Code running in the newly created child process
    {
        ptrace(PTRACE_TRACEME, 0, NULL, NULL);  // Tell kernel: let parent trace me
        execvp(argv[1], &argv[1]);  // Replace child with target program
        return (0);  // Only reached if execvp fails
    }
    // Parent process continues here, tracing the child
    while (1)  // Infinite loop: keep tracing until child exits
    {
        wait(&status);  // Wait for child to stop (at next syscall entry/exit)
        if (WIFEXITED(status))  // Macro: true if child terminated normally
            break;  // Child is done; exit tracing loop
        ptrace(PTRACE_GETREGS, pid, NULL, &regs);  // Copy child CPU registers to regs
        // At this point, regs.orig_rax contains the syscall number
        // regs.rdi, regs.rsi, regs.rdx contain first 3 arguments
        if (regs.orig_rax == SYS_write)  // If syscall is write()
            dprintf(2, "write(%d, %p, %llu)\n", regs.rdi, (void *)regs.rsi, regs.rdx);
        else if (regs.orig_rax == SYS_read)  // If syscall is read()
            dprintf(2, "read(%d, %p, %llu)\n", regs.rdi, (void *)regs.rsi, regs.rdx);
        else if (regs.orig_rax == SYS_open)  // If syscall is open()
            dprintf(2, "open(%p, %d, %d)\n", (void *)regs.rdi, regs.rsi, regs.rdx);
        else if (regs.orig_rax == SYS_exit)  // If syscall is exit()
            dprintf(2, "exit(%d)\n", regs.rdi);
        else  // Unknown or unhandled syscall
            dprintf(2, "%lld\n", regs.orig_rax);  // Just print syscall number
        ptrace(PTRACE_SYSCALL, pid, NULL, NULL);  // Resume child, stop at next syscall
    }
    return (0);  // Traced program finished; exit tracer normally
}
```

## Line-by-Line Translation
| Line | Code | Plain English |
|------|------|--------------|
| 21-25 | (includes) | Headers for ptrace, wait, syscall numbers, register structures |
| 27 | `int main(int argc, char **argv)` | Entry point with command arguments |
| 29 | `int status;` | Variable to receive child process status from wait() |
| 31 | `struct user_regs_struct regs;` | Structure that holds CPU register values |
| 33 | `if (argc < 2)` | Must have program to trace |
| 35 | `pid_t pid = fork();` | Create child process; returns 0 to child, child's PID to parent |
| 36 | `if (pid == 0)` | True in child process |
| 38 | `ptrace(PTRACE_TRACEME, ...)` | Child tells kernel to allow tracing |
| 39 | `execvp(argv[1], &argv[1])` | Replace child process with target program |
| 42 | `while (1)` | Parent loops to trace each syscall |
| 44 | `wait(&status)` | Parent waits for child to stop at syscall |
| 45 | `if (WIFEXITED(status))` | Check if child has exited |
| 47 | `ptrace(PTRACE_GETREGS, ...)` | Copy child's CPU registers into regs struct |
| 48-57 | (syscall dispatch) | Match syscall number and print its name/arguments |
| 58 | `ptrace(PTRACE_SYSCALL, ...)` | Continue child until next syscall stop |

## Common Traps
- Not handling `ptrace` return values correctly.
- Forgetting to `wait()` for child.
- Not using `orig_rax` for syscall number (rax is return value).
- Memory address formatting issues.
