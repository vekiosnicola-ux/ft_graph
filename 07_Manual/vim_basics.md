---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# Vim Editor

---
tags:
  - [Manual, gray]
---

> ~={blue} The 42 editor =~

## Navigation
← [[C11_Index|Vault Home]]

## Modes
| Mode | Enter | Exit |
|------|-------|------|
| Normal | `Esc` | - |
| Insert | `i` | `Esc` |
| Visual | `v` | `Esc` |
| Command | `:` | `Enter` |

## Essential Commands
| Command | Action |
|---------|--------|
| `:w` | Save |
| `:q` | Quit |
| `:wq` | Save & quit |
| `:q!` | Quit without saving |
| `dd` | Delete line |
| `yy` | Copy line |
| `p` | Paste |
| `u` | Undo |
| `/pattern` | Search |
| `n` | Next match |

## Navigation
| Key | Action |
|-----|--------|
| `h j k l` | Left, Down, Up, Right |
| `0` | Start of line |
| `$` | End of line |
| `gg` | Start of file |
| `G` | End of file |

How do you save and quit vim?
::
`:wq` or `:x` or `ZZ`

## Related
- 07_Manual/compilation|Compilation
