---
tags: [CheatSheet, Snippet]
date: 2026-03-29
status: complete
---


# read_bytes.c

```c
 <stdio.h>
 <stdlib.h>

typedef struct filet {
    char s[8];
} FILETIME;
int main(void) {
    FILE *file = fopen("read_bytes.c", "rb");
    size_t offset = 0x001C;
    size_t len = 8;
    unsigned char buffer[len + 1]; // note: 1 byte

    fseek(file, offset, SEEK_SET);
    FILETIME* temp = malloc(sizeof(FILETIME));
    fread(temp, 1, len, file);

    printf("%s\n", temp);
}
```
