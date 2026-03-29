---
tags: []
date: 2026-03-29
status: complete
---
# maff_revalpha

EXAMS INDEX|Exam INDEX | Level 0

---
tags: [Exams, Level_0, magenta]
---


## What it does
Prints the reverse alphabet, alternating case: `ZyXwVuTsRqPoNmLkJiHgFeDcBa`

## Insight
This combines reverse iteration with alternating case. The key insight is:
1. Start at 'z' and go backwards to 'a'
2. Alternate case based on position (even/odd)
3. Use the ASCII difference of 32 to toggle case

The even/odd determination uses `i % 2 == 0` where position 0 is even (lowercase) and position 1 is odd (uppercase).

## Step-by-step Algorithm
1. Initialize letter = 'z' and position = 0
2. While letter >= 'a':
   - If position is even (0, 2, 4, ...): output lowercase letter
   - If position is odd (1, 3, 5, ...): output uppercase letter (letter - 32)
   - Decrement letter
   - Increment position
3. When letter < 'a', exit

## Code
```c
 <unistd.h>       // Required for write() system call

void maff_revalpha(void)   // Function takes no parameters
{
    char c = 'z';           // Start with lowercase 'z' (going backwards)
    int i = 0;              // Position counter: 0,1,2,3... (even/odd tracker)
    
    while (c >= 'a')        // Loop while letter is within alphabet range
    {
        if (i % 2 == 0)     // If position is EVEN (0,2,4...): lowercase
            write(1, &c, 1);           // Write lowercase letter directly
        else                 // If position is ODD (1,3,5...): uppercase
            write(1, &(c - 32), 1);    // Write uppercase: subtract 32 from ASCII
        c--;                 // Move to previous letter in alphabet
        i++;                 // Increment position counter
    }
    write(1, "\n", 1);      // Print final newline
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|-------------|
| 1 | `#include <unistd.h>` | Include header for `write()` system call |
| 3 | `void maff_revalpha(void)` | Define function with no parameters |
| 4 | `{` | Start of function body |
| 5 | `char c = 'z';` | Initialize current letter to 'z' |
| 6 | `int i = 0;` | Initialize position counter to 0 |
| 8 | `while (c >= 'a')` | Loop while letter is within alphabet range |
| 9 | `{` | Start of while body |
| 10 | `if (i % 2 == 0)` | Check if position is even (0, 2, 4...) |
| 11 | `write(1, &c, 1);` | Write lowercase letter directly |
| 12 | `else` | Position is odd (1, 3, 5...) |
| 13 | `write(1, &(c - 32), 1);` | Write uppercase version (ASCII: 'a'-32='A') |
| 14 | `c--;` | Move to previous letter ('z'→'y'→...→'a') |
| 15 | `i++;` | Increment position counter |
| 16 | `}` | End of while body |
| 17 | `write(1, "\n", 1);` | Print newline after output |
| 18 | `}` | End of function |

## Common Traps
- ❌ Starting at 'Z' instead of 'z'
- ❌ Using while (c > 'a') instead of while (c >= 'a') (misses 'a')
- ❌ Getting the even/odd logic backwards
- ❌ Forgetting to decrement c and increment i
- ❌ Not writing the final newline
- ❌ Using printf instead of write
- ❌ Miscalculating the uppercase conversion

## Propedeuticity
- [[maff_alpha]] - Understanding alternating case pattern
- [[ft_countdown]] - Reverse iteration foundation

## Related Exercises
- [[maff_alpha]] - Same but forward: aBcDeFgHiJkLmNoPqRsTuVwXyZ

(End of file - 78 lines)
