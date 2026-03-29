---
tags: []
date: 2026-03-29
status: complete
---
# maff_alpha

EXAMS INDEX|Exam INDEX | Level 0

---
tags: [Exams, Level_0, magenta]
---


## What it does
Prints the alphabet, alternating case: `aBcDeFgHiJkLmNoPqRsTuVwXyZ`

## Insight
This teaches you how to alternate between two states (lowercase/uppercase) while iterating. The key insight is using a counter to determine whether to output lowercase or uppercase for each letter.

The even/odd determination uses `i % 2 == 0` where position 0 is even (lowercase) and position 1 is odd (uppercase). The ASCII difference between uppercase and lowercase letters is 32.

## Step-by-step Algorithm
1. Initialize letter = 'a' and position = 0
2. While letter <= 'z':
   - If position is even (0, 2, 4, ...): output lowercase letter
   - If position is odd (1, 3, 5, ...): output uppercase letter (letter - 32)
   - Increment letter
   - Increment position
3. When letter > 'z', exit

## Code
```c
 <unistd.h>       // Required for write() system call

void maff_alpha(void)      // Function takes no parameters
{
    char c = 'a';           // Start with lowercase 'a'
    int i = 0;              // Position counter: 0,1,2,3... (even/odd tracker)
    
    while (c <= 'z')        // Loop through all lowercase letters
    {
        if (i % 2 == 0)     // If position is EVEN (0,2,4...): lowercase
            write(1, &c, 1);           // Write lowercase letter directly
        else                 // If position is ODD (1,3,5...): uppercase
            write(1, &(c - 32), 1);    // Write uppercase: subtract 32 from ASCII
        c++;                 // Move to next letter in alphabet
        i++;                 // Increment position counter
    }
    write(1, "\n", 1);      // Print final newline
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|-------------|
| 1 | `#include <unistd.h>` | Include header for `write()` system call |
| 3 | `void maff_alpha(void)` | Define function with no parameters |
| 4 | `{` | Start of function body |
| 5 | `char c = 'a';` | Initialize current letter to 'a' |
| 6 | `int i = 0;` | Initialize position counter to 0 |
| 8 | `while (c <= 'z')` | Loop while letter is within alphabet range |
| 9 | `{` | Start of while body |
| 10 | `if (i % 2 == 0)` | Check if position is even (0, 2, 4...) |
| 11 | `write(1, &c, 1);` | Write lowercase letter directly |
| 12 | `else` | Position is odd (1, 3, 5...) |
| 13 | `write(1, &(c - 32), 1);` | Write uppercase version (ASCII: 'a'-32='A') |
| 14 | `c++;` | Move to next letter ('a'→'b'→...→'z') |
| 15 | `i++;` | Increment position counter |
| 16 | `}` | End of while body |
| 17 | `write(1, "\n", 1);` | Print newline after output |
| 18 | `}` | End of function |

## Common Traps
- ❌ Starting at 'A' instead of 'a'
- ❌ Getting the even/odd logic backwards
- ❌ Forgetting to increment both c and i
- ❌ Not writing the final newline
- ❌ Using printf instead of write
- ❌ Miscalculating the uppercase conversion (should be -32, not +32)

## Propedeuticity
- [[hello]] - Basic write output
- [[ft_print_numbers]] - Simple loop iteration

## Related Exercises
- [[maff_revalpha]] - Same pattern but reverse: ZyXwVuTsRqPoNmLkJiHgFeDcBa

(End of file - 75 lines)
