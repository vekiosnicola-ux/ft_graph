---
tags: []
date: 2026-03-29
status: complete
---
# Recursion

---
tags: [Concepts, blue]
---

## What is Recursion?

A function that calls itself until a base case stops it. Each call has its own stack frame with separate variables.

## The Two Essential Parts

```c
// 1. Base case: when to stop
// 2. Recursive case: call itself with simpler input
```

## Why Recursion Works for ft_putnbr

From C00 ex07 `ft_putnbr`:

```c
void ft_putnbr(int nb)
{
    long long n = (nb < 0) ? -(long long)nb : (long long)nb;
    
    if (n >= 10)
        ft_putnbr(n / 10);  // Recursive call with simpler problem
    
    char c = (n % 10) + '0';
    write(1, &c, 1);
}
```

**Why recursion here?** Printing digits in correct order:
- 123: Need to print "1" before "2" before "3"
- Recursion: `ft_putnbr(12)` prints "12", then we print "3"
- The calls stack up, then unwind in reverse order

## The Call Stack Visualization

```
ft_putnbr(123)
  → ft_putnbr(12)
    → ft_putnbr(1)
      → base case reached
    ← return
    → print '1'
  ← return
  → print '2'
← return
→ print '3'
```

Output: "123" ✅

## ft_print_memory: Recursive Address Printing

From C02 ex12 `ft_print_memory`:

```c
void print_addr(unsigned long addr)
{
    char *hex = "0123456789abcdef";
    
    if (addr >= 16)
        print_addr(addr / 16);  // Print higher digits first
    
    write(1, &hex[addr % 16], 1);  // Print this digit
}
```

Same principle: let recursion handle the "before" part.

## Recursion vs Iteration

The invisible skeleton ([[invisible_skeleton]]) applies:

```c
// Iterative (explicit state)
int i = 0;
while (i < 10)
{
    do_something(i);
    i++;
}

// Recursive (implicit state via call stack)
void recurse(int i)
{
    if (i >= 10)
        return;
    do_something(i);
    recurse(i + 1);
}
```

## Recursive Fibonacci

```c
int fib(int n)
{
    if (n <= 1)          // Base case
        return n;
    return fib(n - 1) + fib(n - 2);  // Two recursive calls
}
```

This creates a tree of calls. Note: inefficient for large n (calls grow exponentially).

## flood_fill: Recursive Maze Filling

From textbook Level 4 exercise:

```c
void flood_fill(char **map, int x, int y, char target)
{
    if (x < 0 || y < 0 || map[y][x] == '\0' || map[y][x] != target)
        return;  // Base case: out of bounds or not fillable
    
    map[y][x] = 'F';  // Fill this cell
    
    flood_fill(map, x + 1, y, target);  // Right
    flood_fill(map, x - 1, y, target);  // Left
    flood_fill(map, x, y + 1, target);  // Down
    flood_fill(map, x, y - 1, target);  // Up
}
```

The recursion explores in all four directions, like water spreading.

## Stack Overflow

Each recursive call uses stack space. Too many calls:

```c
void infinite_recursion(void)
{
    infinite_recursion();  // Will eventually crash with stack overflow
}
```

For 42 exercises, depth is usually small (digits of a number, tree height, etc.).

## Key Takeaway

Recursion solves problems where:
1. The problem can be broken into smaller versions of itself
2. There's a clear base case where recursion stops
3. The "before" work needs to happen after the recursive call (reversing order)

The call stack naturally reverses order—useful for printing numbers, addresses, or traversing structures.

---

**Related:** [[invisible_skeleton]], [[pointers]], [[malloc]], [[linked_lists]]
