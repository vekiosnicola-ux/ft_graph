---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# Common Mistakes Log

---
tags: [Tracking, brown]
---

> ~={red} Learn from errors =~

## Navigation
← [[C11_Index|Vault Home]]

## Mistakes by Category

### Pointer Mistakes
| Date | Exercise | Mistake | Fix |
|------|----------|---------|-----|
| - | ft_swap | Forgot to dereference | Use `*a` not `a` |
| - | ft_ft | Changed pointer not value | `*nbr = 42` not `nbr = 42` |

### String Mistakes
| Date | Exercise | Mistake | Fix |
|------|----------|---------|-----|
| - | ft_strlen | Forgot null check | `while (str[i] != '\0')` |
| - | ft_strcpy | Forgot to null-terminate | `dest[i] = '\0'` after loop |

### Memory Mistakes
| Date | Exercise | Mistake | Fix |
|------|----------|---------|-----|
| - | ft_strdup | Forgot +1 for `\0` | `malloc(len + 1)` |
| - | ft_split | Memory leak | Free all allocations |

### Logic Mistakes
| Date | Exercise | Mistake | Fix |
|------|----------|---------|-----|
| - | ft_print_comb | Trailing comma | Check last combination |
| - | ft_putnbr | INT_MIN overflow | Use `long long` |

What is the most common pointer mistake?
::
Forgetting to dereference: using `a = b` instead of `*a = *b`

## Related
- 05_Tracking/Struggle_Areas|Struggle Areas
