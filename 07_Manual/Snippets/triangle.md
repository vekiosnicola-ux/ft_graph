---
tags: [CheatSheet, Snippet]
date: 2026-03-29
status: complete
---


# triangle.c

```c
x,i,j;void f(int h){for(x=0;x<=h;x++){for(j=i;j<h;j++)printf(" "); \
for(i=0;i<x;i++)printf("%c",45-2*(!i||i==x-1||x==h));printf("\n");}}

int main(void) {
    f(8);
}
```
