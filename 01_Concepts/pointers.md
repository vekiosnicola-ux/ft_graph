---
tags: []
date: 2026-03-29
status: complete
---
# Pointers: The Foundation of C

---
tags: [Concepts, blue]
---

## The Core Insight

**Memory is an enormous array of bytes.** A pointer is simply an integer index (an address) into this massive array. This single realization makes the entire C language comprehensible.

When you write `int *p`, you're declaring a variable that stores a coordinate—a location in memory where some data resides.

## Two Fundamental Operations

### 1. `p = &x` — Change WHERE the pointer points

```c
int x = 42;
int *p;
p = &x;  // Put x's address INTO p
```

This stores the **address** of `x` inside `p`. It changes the pointer itself, not the data.

### 2. `*p = 42` — Change the VALUE at that address

```c
int x = 0;
int *p = &x;
*p = 42;  // Go to where p points and write 42 there
// Now x == 42
```

This dereferences the pointer and writes to the destination.

## Why `&c` Matters in write()

From [[write_syscall]]:

```c
// ❌ WRONG - passes VALUE (e.g., 97 for 'a')
write(1, c, 1);  // CPU reads from address 97 → CRASH

// ✅ CORRECT - passes ADDRESS
write(1, &c, 1);  // CPU reads from address of c → works
```

The `write` syscall needs an address to read from, not the value itself.

## Pointers vs Arrays

| Aspect | Pointer | Array |
|--------|---------|-------|
| Storage | Has its own memory for the address | Name maps directly to address (no extra storage) |
| Reassignment | `p = &y` works | `arr = ptr` is illegal (like `5 = 10`) |
| Decay | N/A | `arr` becomes `&arr[0]` when passed to functions |

```c
int arr[5] = {1, 2, 3, 4, 5};
int *p = arr;  // OK - pointer receives array's starting address
arr = p;       // ❌ COMPILE ERROR - array name cannot be reassigned
```

## The Swap Pattern

From C01 ex02 `ft_swap`:

```c
void ft_swap(int *a, int *b)
{
    int temp;
    temp = *a;   // Store value at a's address
    *a = *b;     // Overwrite with value at b's address
    *b = temp;   // Put original a value at b's address
}
```

Without pointers, swap would modify copies, not originals.

## Pointer Chain: The Ultimate Test

From C01 ex01 `ft_ultimate_ft`:

```c
void ft_ultimate_ft(int **********nbr)
{
    **********nbr = 42;  // Dereference ALL 9 levels
}
```

Each `*` is another level of indirection. You must dereference all of them to reach the actual integer.

## Pointer Arithmetic

```c
int arr[3] = {10, 20, 30};
int *p = arr;

p[0]      // Same as *(p + 0) → 10
*(p + 1)  // Same as p[1] → 20
*(p + 2)  // Same as p[2] → 30
```

`array[i]` is syntactically equivalent to `*(array + i)`.

## NULL Pointer

```c
int *p = NULL;
*p = 42;  // CRASH - dereferencing NULL (address 0)
```

NULL is address 0. The CPU prevents access to it, causing a crash instead of returning garbage data. See [[null_terminator]] for contrast.

## Key Takeaway

Understanding pointers as memory indices transforms C from confusing syntax into logical memory manipulation. Every variable lives somewhere in the byte-array we call memory, and pointers are how we find and manipulate that "somewhere."

---

**Related:** [[write_syscall]], [[null_terminator]], [[invisible_skeleton]], [[malloc]]
