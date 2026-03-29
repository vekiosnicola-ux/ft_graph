---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# Makefile

---
tags: [C09, magenta]
---

## Navigation
← [[ft_putchar|ft_putchar]] | [[libft|Next: libft →]]

## What it does
Create a Makefile to compile a C program with proper rules.

## The Insight
Makefiles automate compilation. They define rules with targets, dependencies, and commands. The compiler (`cc`) and flags (`-Wall -Wextra -Werror`) produce the executable.

## Basic Structure
```makefile
NAME = program
CC = cc
CFLAGS = -Wall -Wextra -Werror
SRCS = main.c file1.c file2.c
OBJS = $(SRCS:.c=.o)

all: $(NAME)

$(NAME): $(OBJS)
	$(CC) $(CFLAGS) -o $(NAME) $(OBJS)

clean:
	rm -f $(OBJS)

fclean: clean
	rm -f $(NAME)

re: fclean all

.PHONY: all clean fclean re
```

## Required Rules
| Rule | Purpose |
| :--- | :--- |
| `all` | Default target, builds the program |
| `clean` | Removes object files |
| `fclean` | Removes executable and objects |
| `re` | Rebuilds from scratch |

## Common Traps
- ❌ Missing `-o` flag for output filename.
- ❌ Not using variables for source files (hardcoding).
- ❌ Forgetting `.PHONY` for non-file targets.
- ❌ Wrong order of dependencies in rules.

## Related Concepts
- 07_Manual/compilation|Compilation
- 07_Manual/norminette|Norminette

## Related Exercises
- [[ft_putchar]]
- [[libft]]

What are the required Makefile rules?
::
`all`, `clean`, `fclean`, `re` - plus `.PHONY` declaration
