---
tags: [, algorithm, parsing, rush]
date: 2026-03-29
status: complete
---
# 42 Rush 02: Configuration and Review

**Project:** Rush-02 (C Piscine)
**Tags:** #42piscine   

## Core Curriculum Concepts
This project perfectly marries multiple complex C fundamentals taught throughout the Piscine tracks:

### 1. Program Arguments (`argc` & `argv`)
- **Origin:** Matches concepts learned in C06 (e.g., `ft_print_params`).
- **Application:** We use `argc` to dictate flow. If `argc == 2`, we convert the first argument using `numbers.dict`. If `argc == 3`, we use the dictionary path provided in `argv[1]`.

### 2. String Comparisons and Utilities
- **Origin:** Matches concepts in C01 string length, and C03 comparisons.
- **Application:** Because `#include <string.h>` is forbidden, custom implementations of [[ft_strcmp]] and [[ft_strlen]] are crucial. String comparison controls exactly how we dynamically group base-10 magnitude words.

### 3. Dynamic Memory Allocation (`malloc` & `free`)
- **Origin:** Introduces concepts finalized in C07 (e.g., `ft_strdup`).
- **Application:** Exact buffer sizing safely prevents memory leaks. We dynamically build `char *buffer` elements when constructing strings like `"1000"` mathematically via lengths.

### 4. Advanced Data Structures: Linked Lists
- **Origin:** An early preview of the core systems taught in C12 (List structures).
- **Application:** Evaluators frequently test dictionaries with bizarre empty lines, varying custom keywords, and totally shuffled mapping sequences. `t_dict *head` allows us to securely parse *n-length* files linearly from disk into RAM.

### 5. Standard System I/O (`open`, `read`, `close`)
- **Application:** To securely navigate file size allocations without native `fopen()` functionality, memory reads manually track byte progression.

---
*Created via Antigravity directly to vault mapping.*
