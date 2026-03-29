---
tags: []
date: 2026-03-29
status: complete
---
# Rush00

---
tags:
  - Rush
  - Rush00
  - purple
---

## What it Does

Rush00 is a group project that involves creating a function `rush(int x, int y)` which prints a rectangular pattern to the terminal. The rectangle has specific characters for corners, edges, and interior:

- **Corners**: `'o'`
- **Top/Bottom edges**: `'-'`
- **Left/Right edges**: `'|'`
- **Interior**: `' '` (space)

The function must handle any positive integer values for `x` (width) and `y` (height) and must never crash or enter an infinite loop.

---

## The Insight

The "aha!" moment is realizing that the rectangle is a grid where:
1. The first and last rows are special (all edges/corners)
2. The first and last columns are special (vertical edges)
3. Everything in between is the interior

The problem is essentially about detecting **position** within the grid and printing the appropriate character for that position.

---

## Algorithm

```
For each row i from 0 to y-1:
    For each column j from 0 to x-1:
        Determine character based on position:
        - If (i == 0 or i == y-1) AND (j == 0 or j == x-1): corner 'o'
        - Else if (i == 0 or i == y-1): top/bottom edge '-'
        - Else if (j == 0 or j == x-1): left/right edge '|'
        - Else: interior space ' '
    Print newline
```

### Edge Cases
- `x = 1` or `y = 1`: Single column/row should still show corners and edges correctly
- Minimum values should still produce valid output

---

## The Code

```c
// ============================================
// SECTION 1: HEADER AND helper function
// ============================================

//  pulls in the unistd.h library for write()
// This gives us access to the write() system call
 <unistd.h>

// ft_putchar: Helper function to print a single character
// Parameters: char c - the character to print
// Returns: void (nothing)
// Why use write() instead of printf? In 42 projects, printf is forbidden.
// write() is a low-level system call that writes directly to file descriptor 1 (stdout)
// Syntax: write(file_descriptor, address_of_data, number_of_bytes)
void    ft_putchar(char c)
{
    write(1, &c, 1);  // 1 = stdout, &c = address of char, 1 = write 1 byte
}

// ============================================
// SECTION 2: MAIN rush() FUNCTION
// ============================================

// rush: Prints a rectangle of characters with specified width (x) and height (y)
// Parameters: 
//   - int x: width (number of columns)
//   - int y: height (number of rows)
// Returns: void (prints directly to stdout)
//
// Rectangle layout:
//   o---o    <-- top row: corner, edges, corner
//   |   |    <-- middle rows: edge, spaces, edge
//   |   |
//   o---o    <-- bottom row: corner, edges, corner
void    rush(int x, int y)
{
    int i;  // i = current row index (0 to y-1)
    int j;  // j = current column index (0 to x-1)

    // GUARD CLAUSE: Handle invalid inputs
    // If x or y is zero or negative, do nothing and return
    // This prevents crashes or infinite loops with bad input
    if (x <= 0 || y <= 0)
        return;
    
    // Initialize row counter to 0
    i = 0;
    
    // OUTER LOOP: Iterate through each row from top to bottom
    // Loop as long as i is less than y (number of rows)
    while (i < y)
    {
        // Reset column counter to 0 at the start of each new row
        j = 0;
        
        // INNER LOOP: Iterate through each column from left to right
        // Loop as long as j is less than x (number of columns)
        while (j < x)
        {
            // ========================================
            // POSITION DETECTION LOGIC
            // Check WHERE we are in the rectangle
            // ========================================
            
            // CONDITION 1: CORNERS (checked FIRST - most specific)
            // A corner is when we're on the top/bottom row AND left/right column
            // (i == 0)          = top row
            // (i == y - 1)      = bottom row
            // (j == 0)          = left column
            // (j == x - 1)      = right column
            // We use OR (||) because a corner is on both a special row AND special column
            if ((i == 0 || i == y - 1) && (j == 0 || j == x - 1))
                ft_putchar('o');  // Print corner character
            
            // CONDITION 2: TOP OR BOTTOM EDGE
            // If we're on the top row (i == 0) OR bottom row (i == y - 1)
            // but NOT in a corner position (previous condition failed)
            else if (i == 0 || i == y - 1)
                ft_putchar('-');  // Print horizontal edge character
            
            // CONDITION 3: LEFT OR RIGHT EDGE
            // If we're on the left column (j == 0) OR right column (j == x - 1)
            // but NOT on top/bottom edge (previous condition failed)
            else if (j == 0 || j == x - 1)
                ft_putchar('|');  // Print vertical edge character
            
            // CONDITION 4: INTERIOR (default case)
            // If we reach here, we're not on any edge or corner
            // So we print a space character
            else
                ft_putchar(' ');  // Print interior space
            
            // Move to the next column
            j++;  // j = j + 1 (shorthand)
        }
        
        // After finishing a row, print a newline character to move to next line
        ft_putchar('\n');
        
        // Move to the next row
        i++;  // i = i + 1 (shorthand)
    }
}
```

## Line-by-Line Translation

| Line | Code | Plain English Translation |
|------|------|--------------------------|
| 49 | `#include <unistd.h>` | "Include the Unix standard library header so we can use write()" |
| 51-53 | `ft_putchar(char c)` | "Define a helper function named ft_putchar that takes one character parameter" |
| 52 | `write(1, &c, 1);` | "Write to standard output (file descriptor 1) the character at address c, sending exactly 1 byte" |
| 56-82 | `void rush(int x, int y)` | "Define the main function named rush that takes width x and height y as integers, returns nothing" |
| 58-59 | `int i; int j;` | "Create two integer variables: i for tracking rows, j for tracking columns" |
| 61-62 | `if (x <= 0 \|\| y <= 0) return;` | "If either dimension is zero or negative, stop immediately and don't print anything" |
| 63 | `i = 0;` | "Start at the first row (row index 0)" |
| 64 | `while (i < y)` | "Keep looping as long as we haven't printed all rows" |
| 66 | `j = 0;` | "For each new row, start at the first column (column index 0)" |
| 67 | `while (j < x)` | "Keep looping as long as we haven't printed all columns in this row" |
| 69 | `if ((i == 0 \|\| i == y-1) && (j == 0 \|\| j == x-1))` | "Are we at a corner? (Top or bottom row AND left or right column?)" |
| 70 | `ft_putchar('o');` | "Yes corner: print the letter o" |
| 71-72 | `else if (i == 0 \|\| i == y - 1)` | "No corner, but are we on top or bottom edge?" |
| 73 | `ft_putchar('-');` | "Yes edge: print a dash character" |
| 74-75 | `else if (j == 0 \|\| j == x - 1)` | "No top/bottom edge, but are we on left or right edge?" |
| 76 | `ft_putchar('\|');` | "Yes side edge: print a vertical bar character" |
| 77-78 | `else ft_putchar(' ');` | "Not on any edge: print a space (interior of rectangle)" |
| 79 | `j++;` | "Move to the next column in this row" |
| 80 | `ft_putchar('\n');` | "Finished this row: print a newline to start a new line" |
| 81 | `i++;` | "Move to the next row" |

## Wiki-Links to Related Concepts

- C00/ex04 - ft_is_negative (basic conditional logic)
- C00/ex05 - ft_print_comb (nested loops structure)
- C00/ex06 - ft_print_comb2 (nested loops pattern)
- C01/ex02 - ft_swap (understanding loop variables)
- 02_FONDAMENTALI#Lo Scheletro Invisibile - The "Invisible Skeleton" pattern (while loops)

### Example Output (rush(5, 3))
```
oooo-o
|   |
|   |
oooo-o
```

Wait, that's not right. Let me fix:

```
o---o
|   |
|   |
o---o
```

---

## Common Traps

- ❌ **Wrong corner/edge logic**: Corners must be checked BEFORE edges, otherwise corners might be overwritten
- ❌ **Infinite loop**: Forgetting to increment `i` or `j` variables
- ❌ **Off-by-one errors**: Using `<=` instead of `<` for loop conditions (causes extra row/column)
- ❌ **Not handling edge cases**: `x = 1` or `y = 1` can produce unexpected output if logic isn't correct
- ❌ **Missing newline**: Forgetting to print newline after each row
- ❌ **Wrong character for edges**: Mixing up `-` and `|` positions

---

## Team Strategy

### Division of Labor
1. **Partner A**: Focus on the `rush()` function logic and edge case handling
2. **Partner B**: Create `main.c` for testing and `Makefile` for building

### Suggested Approach
1. **First hour**: 
   - Agree on function signature and behavior
   - Partner A writes the core logic
   - Partner B writes test cases in `main.c`
   
2. **Second hour**:
   - Test with various inputs (1x1, 1x5, 5x1, 5x3, 3x5, etc.)
   - Fix any edge cases
   - Create Makefile

3. **Final hour**:
   - Run norminette to check code style
   - Final testing and cleanup
   - Ensure no memory leaks or crashes with `valgrind`

### Key Communication Points
- Agree on which character represents what BEFORE coding
- Test edge cases together (x=1, y=1, x=0, y=0)
- Use a shared test file to verify both implementations work identically

### Critical Rules
- **Never crash**: Even with x=0 or y=0, function must handle gracefully
- **No infinite loops**: Ensure all loops have proper termination conditions
- **Follow Norm**: No for loops, max 25 lines per function, standard header

---

## File Structure

```
Rush00/
├── rush00.c      # Contains rush() function
├── ft_putchar.c  # Helper function
├── main.c        # Test file (not submitted)
├── Makefile      # Build rules (not submitted)
└── README.md     # This file
```

---

## Related Exercises

- C00/ex04 - ft_is_negative (basic conditional)
- C00/ex05 - ft_print_comb (nested loops)
- C00/ex06 - ft_print_comb2 (nested loops pattern)
