---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# Norminette

---
tags:
  - [Manual, gray]
---

> ~={red} 42 coding standard =~

## Navigation
← [[C11_Index|Vault Home]]

## Rules

### Forbidden
- ❌ `for` loops (use `while`)
- ❌ `printf` (use `write`)
- ❌ Comments inside functions
- ❌ More than 25 lines per function
- ❌ More than 5 functions per file
- ❌ More than 4 parameters per function
- ❌ Global variables

### Required
- ✅ 42 header in every file
- ✅ `while` loops only
- ✅ `write()` for output
- ✅ Proper indentation (tabs)
- ✅ No trailing whitespace

## Header Format
```c
/* ************************************************************************** */
/*                                                                            */
/*                                                        :::      ::::::::   */
/*   filename.c                                         :+:      :+:    :+:   */
/*                                                    +:+ +:+         +:+     */
/*   By: username <email>                           +#+  +:+       +#+        */
/*                                                +#+#+#+#+#+   +#+           */
/*   Created: 2024/01/01 00:00:00 by username          #+#    #+#             */
/*   Updated: 2024/01/01 00:00:00 by username         ###   ########.fr       */
/*                                                                            */
/* ************************************************************************** */
```

What loops are allowed in 42?
::
Only `while` loops. `for` and `do...while` are forbidden.

## Related
- 07_Manual/compilation|Compilation
- 07_Manual/moulinette|Moulinette
