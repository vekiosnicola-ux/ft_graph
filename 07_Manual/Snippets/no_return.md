---
tags: [CheatSheet, Snippet]
date: 2026-03-29
status: complete
---


# no_return.c

```c
 <stdio.h>

f(n) {*&n*=2;}

int main(void) {
    printf("%d\n", f(0b10101));
}
```
