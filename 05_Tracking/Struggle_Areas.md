---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# Struggle Areas

---
tags: [Tracking, brown]
---

> ~={red} Focus here for maximum improvement =~

## Navigation
← [[C11_Index|Vault Home]]

## Current Struggles
<!-- Update this as you practice -->

### Pointers
- [ ] Understanding `*` vs `&`
- [ ] Multi-level indirection
- [ ] Pointer arithmetic

### Memory
- [ ] When to use malloc
- [ ] Forgetting to free
- [ ] Buffer overflow

### Strings
- [ ] Null terminator handling
- [ ] Off-by-one errors
- [ ] Edge cases (empty string, NULL)

### Recursion
- [ ] Base case definition
- [ ] Stack overflow prevention
- [ ] Visualizing call stack

What should you do when you struggle?
::
1. Identify the specific concept
2. Find related exercises
3. Practice with flashcards
4. Review common mistakes

## Dataview
```dataview
TABLE struggle-count as Struggles
FROM "02_Modules"
WHERE struggle-count > 0
SORT struggle-count DESC
```
