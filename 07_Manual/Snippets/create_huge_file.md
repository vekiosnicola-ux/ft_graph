---
tags: [CheatSheet, Snippet]
date: 2026-03-29
status: complete
---


# create_huge_file.c

```c
 <stdio.h>
 <stdlib.h>

 SIZE 5000000000UL
int main(int ac, char **av) {
    char *s;

    if (!(s =(char*)malloc(SIZE * sizeof(char))))
           return 1;
    for (size_t i = 0; i < SIZE; i++)
          s[i] = "ABCDEFGHIJ KLMNOP QRSTU VWX YZab cdefghijklmnopo rstuvwxyz!@#$%^"[rand() & 0x3F];
    FILE *fp;

   fp = fopen("test2.txt", "w+");
   fputs(s, fp);
   fclose(fp);

    free(s);
    return 0;
}
```
