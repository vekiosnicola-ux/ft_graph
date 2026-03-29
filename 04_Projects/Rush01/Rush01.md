---
tags: []
date: 2026-03-29
status: complete
---
# Rush01

---
tags:
  - Rush
  - Rush01
  - purple
---

## What it Does

Rush01 is the **Skyscraper Puzzle**. Given a grid of size NxN and clues on each side indicating how many skyscrapers are visible from that direction, the goal is to arrange numbers 1-N in the grid such that:

- Each row contains each number 1-N exactly once
- Each column contains each number 1-N exactly once
- All visible building clues are satisfied

### The Rules
- A building of height K is visible from a direction if all buildings before it have height less than K
- The view count equals how many buildings you can see looking from that side
- Clues are given as: top, bottom, left, right for each row/column

---

## The Insight

The "aha!" moment is understanding that this is a **constraint satisfaction problem** that can be solved with **backtracking**:

1. **Visibility Rule**: A building is visible if it's taller than ALL buildings seen so far from that direction
2. **Backtracking**: Try a number, check if it breaks any constraints, if so backtrack and try another
3. **Pruning**: If a placement violates clue constraints immediately, don't continue down that path

The key optimization is **checking clues as you go** rather than only at the end.

---

## Algorithm

### Grid Representation
```
clues[4][N]  - top, bottom, left, right clues
grid[N][N]   - the solution grid (0 = empty)
```

### Visibility Check Functions
```
count_top_view(col):    count visible from top
count_bottom_view(col): count visible from bottom
count_left_view(row):   count visible from left
count_right_view(row):  count visible from right
```

### Backtracking Solver
```
solve(grid, position):
    if position == N*N:  # filled all cells
        return check_all_clues()
    
    row = position / N
    col = position % N
    
    for num in 1 to N:
        if num not in row AND num not in col:
            grid[row][col] = num
            
            if partial_check(row, col):  # pruning
                if solve(grid, position + 1):
                    return true
            
            grid[row][col] = 0  # backtrack
    
    return false
```

### Partial Check (Pruning)
Before recursing, verify that the visible count so far doesn't exceed the clue:
```
- When filling a row left-to-right, check left clue
- When filling a column top-to-bottom, check top clue
```

---

## The Code

```c
// ============================================
// SECTION 1: HEADERS AND STRUCTURES
// ============================================

//  pulls in required libraries
// unistd.h gives us write() for output
// stdlib.h gives us malloc() for dynamic memory
 <unistd.h>
 <stdlib.h>

// typedef creates a custom type name
// This struct holds all puzzle data:
//   - size: the grid dimension (N for NxN)
//   - clues: array of 4*N clue values (top, bottom, left, right)
//   - grid: 2D array (NxN) holding the puzzle solution
typedef struct s Rush
{
    int size;      // N, the dimension of the grid (e.g., 4 for 4x4)
    int *clues;    // Array of 4*size clues: [0..N-1]=top, [N..2N-1]=bottom, etc.
    int **grid;    // 2D grid: grid[row][col] = number placed (0 = empty)
} t_rush;

// ============================================
// SECTION 2: OUTPUT HELPER
// ============================================

// ft_putchar: Prints a single character to stdout
// Why not printf? In 42 projects, printf is forbidden.
// We use write(), the low-level Unix system call.
// write(file_descriptor, buffer_address, byte_count)
void ft_putchar(char c)
{
    write(1, &c, 1);  // 1 = stdout, &c = address of character, 1 = 1 byte
}

// ============================================
// SECTION 3: VISIBILITY COUNTING
// ============================================

// count_visible: Counts how many buildings are visible looking along a line
// Parameters:
//   - int *line: pointer to array of numbers (a row or column)
//   - int size: how many numbers in the line
// Returns: how many buildings are visible
//
// Visibility rule: A building is visible if it's TALLER than all buildings before it
// Example: line = [3, 1, 2]  looking left to right
//   - First building (3): Always visible, count=1, max=3
//   - Second building (1): Not visible (1 < 3), count stays 1
//   - Third building (2): Visible (2 > 3? NO - wait, 2 < 3)... actually 2 < 3 so NOT visible
//   Wait, let me recalculate:
//   - 3 is visible (count=1, max=3)
//   - 1 is NOT visible (1 < 3)
//   - 2 is NOT visible (2 < 3)
//   So count_visible([3,1,2]) = 1
//
// Example: line = [2, 3, 1]  looking left to right
//   - 2 is visible (count=1, max=2)
//   - 3 is visible (3 > 2, count=2, max=3)
//   - 1 is NOT visible (1 < 3)
//   So count_visible([2,3,1]) = 2
int count_visible(int *line, int size)
{
    int max;    // Track the TALLEST building seen so far
    int count;  // Track how many buildings we've seen
    int i;      // Loop counter (index position in line)

    max = 0;      // No buildings seen yet, so max height is 0
    count = 0;    // Haven't seen any visible buildings yet
    i = 0;        // Start at the first position
    
    // Loop through the entire line from left to right
    while (i < size)
    {
        // Is this building taller than ALL buildings we've seen?
        // If line[i] > max, then this building "sticks out" and is visible
        if (line[i] > max)
        {
            max = line[i];    // Update our record of tallest building
            count++;          // We can see this one!
        }
        i++;  // Move to the next building position
    }
    return (count);  // Return how many visible buildings we counted
}

// ============================================
// SECTION 4: CLUE VALIDATION (PRUNING)
// ============================================

// check_clues_at: Validates clues incrementally as we fill the grid
// Parameters:
//   - t_rush *rush: pointer to puzzle data structure
//   - int row: the row we just filled
//   - int col: the column we just filled
// Returns: 1 if clues still could be satisfied, 0 if we've already failed
//
// PRUNING = "If this move already breaks a rule, don't continue down this path"
// This is the KEY optimization that makes the solver fast
// Instead of checking ALL clues at the end, we check partial clues as we go
//
// The clues array is organized as:
//   [0 to size-1]           = top clues (looking DOWN each column)
//   [size to 2*size-1]     = bottom clues (looking UP each column)
//   [2*size to 3*size-1]   = left clues (looking RIGHT along each row)
//   [2*size + row]          = left clue for a specific row
int check_clues_at(t_rush *rush, int row, int col)
{
    int visible;  // Store the count of visible buildings from current position

    // Have we finished filling this row? (col == size - 1 means last column)
    // Only check row clues when a row is COMPLETE - otherwise we can't count visibility yet
    if (col == rush->size - 1)
    {
        // Count visible buildings in this row (looking from the LEFT)
        visible = count_visible(rush->grid[row], rush->size);
        // Compare against the LEFT clue for this row
        // LEFT clues are stored at index: 2*size + row
        // If visible doesn't match the clue, this solution path is WRONG
        if (visible != rush->clues[2 * rush->size + row])
            return (0);  // FAILED: return 0 to tell caller to backtrack
    }
    
    // Have we finished filling this column? (row == size - 1 means last row)
    // Only check column clues when a column is COMPLETE
    if (row == rush->size - 1)
    {
        // Count visible buildings in this column (looking from the TOP)
        // Note: This assumes we have a helper function count_visible_column()
        visible = count_visible_column(rush->grid, col, rush->size);
        // Compare against the TOP clue for this column
        // TOP clues are stored at index: col
        if (visible != rush->clues[col])
            return (0);  // FAILED: return 0 to tell caller to backtrack
    }
    return (1);  // PASSED so far: keep exploring this solution path
}

// ============================================
// SECTION 5: BACKTRACKING SOLVER
// ============================================

// solve: Recursive function that tries to solve the skyscraper puzzle
// Parameters:
//   - t_rush *rush: pointer to puzzle data
//   - int pos: current position in grid (0 to size*size - 1)
// Returns: 1 if solution found, 0 if no solution exists
//
// ALGORITHM (Backtracking/Depth-First Search):
//   1. If all cells are filled, check if ALL clues match (final validation)
//   2. Otherwise, pick the next empty cell
//   3. Try placing each number 1 to N that doesn't violate row/column uniqueness
//   4. After placing a number, check if clues CAN still be satisfied (pruning)
//   5. If clues are OK, RECURSIVELY try to fill the rest
//   6. If recursive call finds solution, propagate success upward
//   7. If no number works here, UNDO this placement (backtrack) and return failure
//
// Example of backtracking:
//   We try putting 3 at position (0,0)
//   Then we try putting 2 at position (0,1)
//   But then we get stuck (no valid number for (0,2))
//   So we backtrack: remove 2 from (0,1)
//   And try putting 3 at position (0,1) instead...
//   This is why we need to set grid[row][col] = 0 when a path fails
int solve(t_rush *rush, int pos)
{
    int row;  // Current row index (calculated from position)
    int col;  // Current column index (calculated from position)
    int num;  // The number we're trying to place (1 to size)
    int i;    // Loop counter for trying different numbers

    // BASE CASE: Have we filled all cells?
    // pos ranges from 0 to (size*size - 1)
    // When pos == size*size, we've filled the last cell successfully
    if (pos == rush->size * rush->size)
        return (check_all_clues(rush));  // Final check of all clues, return result
    
    // Convert flat position to row and column indices
    // Example: for 4x4 grid, position 6 means row=6/4=1, col=6%4=2
    // This is called "row-major order" - fill row by row, left to right
    row = pos / rush->size;  // Integer division: how many full rows we've passed
    col = pos % rush->size;  // Modulo: position within the current row
    
    // Try each number from 1 to size
    num = 1;
    while (num <= rush->size)
    {
        // Can we place 'num' at position (row, col)?
        // Rules: Each number 1-N must appear exactly once in each row AND column
        // is_in_row(): checks if 'num' already exists in this row
        // is_in_col(): checks if 'num' already exists in this column
        // If neither contains 'num', we CAN try placing it here
        if (!is_in_row(rush->grid[row], num, col) &&
            !is_in_col(rush->grid, col, num, row))
        {
            // Place the number (make a "move")
            rush->grid[row][col] = num;
            
            // PRUNING: Before going deeper, check if this partial solution
            // could still lead to a valid answer
            // This is what makes the algorithm FAST - it cuts dead branches early
            if (check_clues_at(rush, row, col))
            {
                // The partial solution looks promising, so go deeper
                // Try to fill the NEXT position (pos + 1)
                if (solve(rush, pos + 1))
                    return (1);  // SOLUTION FOUND! Propagate success upward
            }
            
            // If we reach here, either:
            // 1. check_clues_at() failed (this path is impossible), OR
            // 2. solve() for the rest of the grid failed (no solution from here)
            // Either way, we need to UNDO our move and try another number
            rush->grid[row][col] = 0;  // Remove our number (backtrack)
        }
        num++;  // Try the next number (1, then 2, then 3, etc.)
    }
    
    // If we tried all numbers and none worked, this position is UNSOLVABLE
    // Signal failure so the caller can backtrack
    return (0);
}
```

## Line-by-Line Translation

| Line | Code | Plain English Translation |
|------|------|--------------------------|
| 79 | `#include <unistd.h>` | "Include Unix standard library for the write() system call" |
| 80 | `#include <stdlib.h>` | "Include standard library for malloc() - dynamic memory allocation" |
| 83-88 | `typedef struct s Rush { ... } t_rush;` | "Define a custom data type called 't_rush' that bundles together: size (grid dimension), clues (array of hint numbers), and grid (2D array of our solution)" |
| 90-93 | `void ft_putchar(char c)` | "Create a helper function that writes one character to screen" |
| 92 | `write(1, &c, 1);` | "System call: send 1 byte from address &c to file descriptor 1 (stdout)" |
| 95-114 | `int count_visible(int *line, int size)` | "Define a function that counts visible buildings in a line - a building is visible if taller than all before it" |
| 97-99 | `int max; int count; int i;` | "Create three variables: max (tallest seen), count (visible count), i (loop index)" |
| 101-102 | `max = 0; count = 0;` | "Start with no buildings seen - max height is 0, visible count is 0" |
| 104 | `while (i < size)` | "Loop through each building in the line" |
| 106 | `if (line[i] > max)` | "Is this building taller than everything we've seen so far?" |
| 108-109 | `max = line[i]; count++;` | "Yes! Update our record of tallest, and increment visible count" |
| 113 | `return (count);` | "Return how many visible buildings we found" |
| 116-135 | `int check_clues_at(t_rush *rush, int row, int col)` | "Check if the clues for this row/column could still be satisfied after placing a number" |
| 121-126 | `if (col == rush->size - 1)` | "Is this the last column of the row? Only check row clues when row is complete" |
| 123 | `visible = count_visible(rush->grid[row], ...)` | "Count visible buildings in this row (looking from left)" |
| 124 | `if (visible != rush->clues[2*size + row])` | "Does visible count match the left clue for this row?" |
| 131 | `if (visible != rush->clues[col])` | "Does visible count match the top clue for this column?" |
| 137-167 | `int solve(t_rush *rush, int pos)` | "The main recursive solver - tries numbers until it finds a valid solution" |
| 144-145 | `if (pos == size*size) return (check_all_clues(...));` | "Base case: if we've filled all cells, do final validation of all clues" |
| 147-148 | `row = pos / size; col = pos % size;` | "Convert position number to row and column: 6 becomes row=1, col=2 in a 4x4 grid" |
| 150-164 | `while (num <= size) { ... }` | "Try each number from 1 to N at this position" |
| 153-154 | `if (!is_in_row(...) && !is_in_col(...))` | "Can we legally place 'num' here? Check row and column for duplicates" |
| 156 | `rush->grid[row][col] = num;` | "Yes: place the number (make a move)" |
| 157 | `if (check_clues_at(...))` | "Pruning check: does this partial solution still look possible?" |
| 159-160 | `if (solve(rush, pos + 1)) return (1);` | "Recursive call: try to fill the rest of the grid. If success, propagate upward" |
| 162 | `rush->grid[row][col] = 0;` | "Backtrack: remove our number - this path didn't work, undo the move" |

## Wiki-Links to Related Concepts

- C03/ex04 - ft_strstr (searching within constraints - similar pattern of finding valid placements)
- C04/ex00 - ft_atoi (parsing command-line input - how we read the clues)
- C07/ex00 - ft_lstnew (linked lists for state - though we use arrays here)
- Exam Level 4 - flood_fill (similar backtracking/recursive approach)
- 02_FONDAMENTALI#Algoritmo di Euclide - The backtracking concept is similar to exploring branches of a tree
- 04B_C00#Lo Scheletro Invisibile - The while loops follow the same pattern as other 42 exercises

---

## Common Traps

- ❌ **Not checking visibility incrementally**: Only checking at the end causes massive slowdown
- ❌ **Forgetting to check row AND column**: Numbers must be unique in both
- ❌ **Wrong visibility algorithm**: Must compare against MAX seen, not just previous
- ❌ **Not pruning early**: This causes exponential slowdown on larger grids
- ❌ **Stack overflow**: Deep recursion on 6x6+ grids may need iterative approach
- ❌ **Not handling no solution**: Some clue combinations are impossible

---

## Team Strategy

### Division of Labor
1. **Partner A**: Focus on visibility counting functions and clue checking
2. **Partner B**: Focus on backtracking solver and grid management

### Suggested Approach

#### Hour 1: Foundation
- Agree on grid representation and data structures
- Partner A writes `count_visible()` and `check_*` functions
- Partner B writes `is_in_row()`, `is_in_col()`, and basic grid setup

#### Hour 2: Core Solver
- Partner A implements backtracking with pruning
- Partner B implements final clue validation
- Both test separately with small grids (4x4)

#### Hour 3: Integration & Optimization
- Merge code, fix conflicts
- Test with 5x5 and 6x6
- Add early exit for impossible puzzles
- Profile and optimize visibility checks

#### Hour 4: Polish
- Add user input handling (clues from arguments)
- Format output correctly
- Run norminette
- Test edge cases

### Key Functions to Test Individually
1. `count_visible()` - verify with known sequences
2. Backtracking - ensure it actually backtracks
3. Clue validation - verify all 4 directions

### Critical Rules
- **Pruning is essential**: Without it, 6x6 takes minutes instead of seconds
- **Handle impossible puzzles**: Some clue sets have no solution
- **Output format**: Match exact specification (space-separated, newline at end)

---

## Example Puzzle

### Input (4x4)
```
./rush01 4 1 2 2 4 3 2 1 3 2 4 3 2 1 3 2 2 4
```
(Top: 1 2 2 4, Bottom: 3 2 1 3, Left: 2 4 3 2, Right: 2 1 3 2)

### Possible Solution
```
1 2 3 4
2 4 3 1
3 1 4 2
4 3 2 1
```

---

## File Structure

```
Rush01/
├── rush01.c      # Main solver and input handling
├── grid_utils.c  # Grid manipulation helpers
├── check.c       # Visibility and clue checking
├── backtrack.c   # Backtracking solver
├── ft_putchar.c  # Output helper
├── Makefile      # Build rules
└── README.md     # This file
```

---

## Related Exercises

- C03/ex04 - ft_strstr (searching within constraints)
- C04/ex00 - ft_atoi (parsing input)
- C07/ex00 - ft_lstnew (linked lists for state)
- Exam Level 4 - flood_fill (similar backtracking concept)
