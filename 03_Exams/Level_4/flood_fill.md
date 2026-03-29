---
tags: [Level_4, exam]
  - recursion
  - algorithm
  - white
---


# flood_fill

## What it does
Recursive flood fill on 2D grid. Fills contiguous area starting from a point.

## The Insight
Base case: if out of bounds or current != target, return. Else: set current to 'F', recursively fill 4 directions (up, down, left, right).

## Step-by-step Algorithm
1. Check bounds (y<0 || y>=size.y || x<0 || x>=size.x)
2. Check if area[y][x] != to_fill: return
3. area[y][x] = 'F'
4. Recurse: fill(x-1,y), fill(x+1,y), fill(x,y-1), fill(x,y+1)

## The Code
```c
// flood_fill: Recursively fills connected area with 'F'
// t_point: struct with 'x' and 'y' integer members
// Fills all connected cells matching 'to_fill' character

void fill(char **area, t_point size, t_point vec, char to_fill)
{
    // BASE CASE: Check all failure conditions first
    // 1. Out of bounds check: y coordinate
    // 2. Out of bounds check: x coordinate
    // 3. Current cell doesn't match target (already filled or different color)
    if (vec.y < 0 || vec.y >= size.y || vec.x < 0 || vec.x >= size.x || area[vec.y][vec.x] != to_fill)
        return;                             // Base case: don't recurse further
    
    area[vec.y][vec.x] = 'F';              // Mark current cell as filled
    
    // RECURSIVE CASE: Fill 4 adjacent cells
    // Use compound literals to create t_point structs for each direction
    fill(area, size, (t_point){vec.x - 1, vec.y}, to_fill);  // LEFT
    fill(area, size, (t_point){vec.x + 1, vec.y}, to_fill);  // RIGHT
    fill(area, size, (t_point){vec.x, vec.y - 1}, to_fill);  // UP
    fill(area, size, (t_point){vec.x, vec.y + 1}, to_fill);  // DOWN
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 21 | `void fill(char **area, t_point size, t_point vec, char to_fill)` | Recursive function: 2D grid, grid size, current position, target character to fill |
| 23-24 | `if (vec.y < 0 \|\| vec.y >= size.y \|\| vec.x < 0 \|\| vec.x >= size.x \|\| area[vec.y][vec.x] != to_fill)` | Bounds check: y<0 or y>=height OR x<0 or x>=width OR cell doesn't match target |
| 24 | `return;` | Base case: stop recursion, cell not fillable |
| 25 | `area[vec.y][vec.x] = 'F';` | Fill the current cell (mark before recursing to avoid infinite loops) |
| 26 | `fill(area, size, (t_point){vec.x - 1, vec.y}, to_fill);` | Recurse LEFT: x-1, same y |
| 27 | `fill(area, size, (t_point){vec.x + 1, vec.y}, to_fill);` | Recurse RIGHT: x+1, same y |
| 28 | `fill(area, size, (t_point){vec.x, vec.y - 1}, to_fill);` | Recurse UP: same x, y-1 |
| 29 | `fill(area, size, (t_point){vec.x, vec.y + 1}, to_fill);` | Recurse DOWN: same x, y+1 |

## Common Traps
- ❌ Infinite recursion (must change cell value BEFORE recursing - without this, re-visits same cell forever)
- ❌ Wrong order of checks (check bounds before checking value - accessing invalid memory otherwise)
- ❌ Not passing correct coordinates (vec.x and vec.y can be confused, order matters)

## Related
- [[sort_int_tab]] - sorting algorithm
- [[brainfuck]] - more recursion practice
- EXAMS INDEX|Exam INDEX
