---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# <string.h> Functions

---
tags:
  - [Manual, gray]
---

> ~={blue} String manipulation library =~

## Navigation
← [[C11_Index|Vault Home]]

## ⚠️ NOT ALLOWED IN 42
You must reimplement these functions yourself!

## Functions

### ft_strlen
```c
size_t strlen(const char *s);
```
Returns length of string (not counting `\0`).

### ft_strcpy
```c
char *strcpy(char *dest, const char *src);
```
Copies src to dest. Returns dest.

### ft_strncpy
```c
char *strncpy(char *dest, const char *src, size_t n);
```
Copies at most n chars. Pads with `\0` if src shorter.

### ft_strcmp
```c
int strcmp(const char *s1, const char *s2);
```
Compares strings. Returns difference at first mismatch.

### ft_strncmp
```c
int strncmp(const char *s1, const char *s2, size_t n);
```
Compares at most n characters.

### ft_strcat
```c
char *strcat(char *dest, const char *src);
```
Appends src to dest. Returns dest.

### ft_strncat
```c
char *strncat(char *dest, const char *src, size_t n);
```
Appends at most n chars from src.

### ft_strstr
```c
char *strstr(const char *haystack, const char *needle);
```
Finds first occurrence of needle in haystack.

### ft_strdup
```c
char *strdup(const char *s);
```
Duplicates string using malloc.

What does strcmp return?
::
- 0 if strings are equal
- Negative if s1 < s2
- Positive if s1 > s2

## Related
- C03/INDEX|C03 String Ops
- C05/INDEX|C05 Memory
