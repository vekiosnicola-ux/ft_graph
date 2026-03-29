---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# libft

---
tags: [C09, magenta]
---

## Navigation
← [[Makefile|Makefile]] | C09_INDEX|C09 INDEX →

## What it does
Create a static library `libft.a` containing basic C functions for reuse across projects.

## The Insight
A static library is a collection of object files (`.o`) bundled into a single archive (`.a`). Using `ar` to create and `ranlib` to index allows linking with `-lft -L.`.

## Step-by-step Algorithm
1. Write C source files with functions (e.g., `ft_putchar.c`, `ft_strlen.c`).
2. Create a Makefile that compiles each `.c` to `.o`.
3. Use `ar rcs libft.a *.o` to create the archive.
4. Use `ranlib libft.a` to create the index.
5. Compile your program with: `cc -L. -lft main.c`

## Makefile for libft
```makefile
NAME = libft.a
CC = cc
CFLAGS = -Wall -Wextra -Werror
AR = ar
ARFLAGS = rcs
SRCS = ft_putchar.c ft_strlen.c ft_strcpy.c
OBJS = $(SRCS:.c=.o)

all: $(NAME)

$(NAME): $(OBJS)
	$(AR) $(ARFLAGS) $(NAME) $(OBJS)

clean:
	rm -f $(OBJS)

fclean: clean
	rm -f $(NAME)

re: fclean all

.PHONY: all clean fclean re
```

## Common Traps
- ❌ Forgetting `ranlib` after `ar`.
- ❌ Wrong order: `ar rcs libft.a *.o` must list objects after the archive name.
- ❌ Not using `-I.` flag if header is in current directory.
- ❌ Forgetting to update Makefile when adding new source files.

## Related Concepts
- 07_Manual/compilation|Compilation
- 07_Manual/norminette|Norminette

## Related Exercises
- [[ft_putchar]]
- [[Makefile]]

How do you create a static library?
::
```bash
ar rcs libft.a *.o
ranlib libft.a
```
