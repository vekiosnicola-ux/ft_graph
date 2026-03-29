---
tags: []
date: 2026-03-29
status: complete
---
# The Invisible Skeleton

---
tags: [Concepts, blue]
---

## The Pattern That Powers 80% of Exercises

The "invisible skeleton" is the underlying structure shared by most 42 exam exercises. Once you recognize it, problems that seemed different become obvious.

## The Three-Phase Structure

```c
// Phase 1: Initialization
int i = 0;

// Phase 2: Loop Condition
while (str[i] != '\0')
{
    // Phase 3: Action + Advancement
    do_something();
    i++;
}
```

1. **Initialize** an index or counter
2. **Loop** while a condition holds
3. **Act** and **advance** in each iteration

## Why It's Called "Invisible"

Students see different problems on the surface:
- `ft_strlen` - counting characters
- `ft_putstr` - printing characters
- `ft_atoi` - converting characters to numbers
- `ft_putnbr` - printing numbers

But beneath, they all follow the same skeleton.

## Example 1: ft_strlen (C01 ex06)

```c
int ft_strlen(char *str)
{
    int i = 0;
    while (str[i] != '\0')  // Phase 2
    {
        i++;                 // Phase 3: advancement
    }
    return i;                // Phase 3: action (return)
}
```

## Example 2: ft_putstr (C01 ex05)

```c
void ft_putstr(char *str)
{
    int i = 0;
    while (str[i] != '\0')   // Phase 2
    {
        write(1, &str[i], 1);// Phase 3: action
        i++;                 // Phase 3: advancement
    }
}
```

Same skeleton, different action.

## Example 3: ft_putnbr (C00 ex07)

```c
void ft_putnbr(int nb)
{
    long long n = (nb < 0) ? -(long long)nb : (long long)nb;
    
    if (n >= 10)
        ft_putnbr(n / 10);   // Recursive skeleton!
    
    char c = (n % 10) + '0';
    write(1, &c, 1);         // Action: print digit
}
```

Recursive version still follows the pattern—recursion replaces iteration.

## Example 4: ft_atoi (not an official exercise but follows pattern)

```c
int ft_atoi(char *str)
{
    int i = 0;
    int sign = 1;
    int result = 0;
    
    while (str[i] == ' ' || str[i] == '\t')  // Skip whitespace
        i++;
    
    if (str[i] == '-' || str[i] == '+')
        sign = (str[i++] == '-') ? -1 : 1;
    
    while (str[i] >= '0' && str[i] <= '9')   // Phase 2
    {
        result = result * 10 + (str[i] - '0'); // Phase 3: action
        i++;                                    // Phase 3: advancement
    }
    return result * sign;
}
```

## Why 42 Bans for loops

The Norminette forbids `for` loops. This forces explicit management of all three phases:

```c
// ❌ Forbidden in 42
for (int i = 0; str[i]; i++)
    write(1, &str[i], 1);

// ✅ Required form
int i = 0;
while (str[i])
    write(1, &str[i], 1), i++;
```

The `while` form makes the skeleton explicit—each phase is visible.

## The Odometer Variation

From C00 ex08 `ft_print_combn`, the skeleton adapts:

```c
while (1)
{
    // Print current state
    print_digits();
    
    // Check if done
    if (is_last_combination())
        break;
    
    // Advance to next state
    increment_rightmost_possible();
}
```

Same phases, different advancement logic.

## Key Takeaway

The invisible skeleton is your friend. When facing a new problem:
1. Identify which phase is different (initialization? condition? advancement?)
2. The rest follows the proven pattern
3. This is why the skeleton is "invisible"—it's everywhere once you see it

---

**Related:** [[pointers]], [[null_terminator]], [[write_syscall]], [[recursion]]
