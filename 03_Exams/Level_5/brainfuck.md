---
tags: [Level_5, exam]
  - interpreter
  - recursion
  - white
---


# brainfuck

## What it does
Interpreter for Brainfuck language. Uses 2048-byte array. Commands: > < + - . , [ ]

## The Insight
Pointer-based state machine. [ ] are while loops with depth tracking for nested loops.

## Step-by-step Algorithm
1. unsigned char mem[2048]={0}, *ptr=mem
2. Loop through program: > ptr++, < ptr--, + (*ptr)++, - (*ptr)--, . write(1,ptr,1)
3. [: if *ptr==0, find matching ] by counting nesting depth
4. ]: if *ptr!=0, find matching [ by counting nesting depth
5. Ignore other chars

## The Code
```c
// brainfuck: Brainfuck language interpreter
// Brainfuck commands:
//   >   Increment pointer (move right)
//   <   Decrement pointer (move left)
//   +   Increment byte at pointer
//   -   Decrement byte at pointer
//   .   Output byte at pointer
//   ,   Input byte to pointer
//   [   If byte at pointer is 0, jump past matching ]
//   ]   If byte at pointer is non-zero, jump back to matching [

void brainfuck(char *s){
    unsigned char m[2048]={0};             // Memory array: 2048 cells, all initialized to 0
    unsigned char *p=m;                    // Pointer: points to current memory cell
    int i=0, depth;                        // i=program counter, depth=nesting level for brackets
    
    while(s[i]){                           // Main interpreter loop: while not end of program
        if(s[i]=='>')p++;                  // > : Move pointer right (to next cell)
        else if(s[i]=='<')p--;             // < : Move pointer left (to previous cell)
        else if(s[i]=='+')(*p)++;          // + : Increment byte at pointer
        else if(s[i]=='-')(*p)--;          // - : Decrement byte at pointer
        else if(s[i]=='.')write(1,p,1);   // . : Output byte at pointer
        else if(s[i]=='['&&!*p){           // [ : If current byte is 0, skip to matching ]
            depth=1;                        // Start counting nesting depth (at least 1 for current])
            while(depth){                   // Find matching ] by counting bracket depth
                i++;                        // Move to next program character
                if(s[i]=='[')depth++;      // Nested [ increases depth
                if(s[i]==']')depth--;      // Matching ] decreases depth
            }
        }
        else if(s[i]==']'&&*p){            // ] : If current byte is non-zero, jump back to matching [
            depth=1;                        // Start counting nesting depth
            while(depth){                   // Find matching [ by counting bracket depth
                i--;                        // Move backwards through program
                if(s[i]==']')depth++;      // Nested ] increases depth
                if(s[i]=='[')depth--;      // Matching [ decreases depth
            }
        }
        i++;                                // Move to next program instruction
    }
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 22 | `void brainfuck(char *s)` | Brainfuck interpreter: takes program string |
| 23 | `unsigned char m[2048]={0};` | Memory array: 2048 bytes, all zero-initialized |
| 24 | `unsigned char *p=m;` | Pointer: current position in memory array |
| 25 | `int i=0, depth;` | i=program counter (which instruction), depth=bracket nesting level |
| 26 | `while(s[i])` | Main loop: execute while not end of program string |
| 27 | `if(s[i]=='>')p++;` | > : Increment pointer (move to next memory cell) |
| 28 | `else if(s[i]=='<')p--;` | < : Decrement pointer (move to previous memory cell) |
| 29 | `else if(s[i]=='+')(*p)++;` | + : Increment byte at current pointer |
| 30 | `else if(s[i]=='-')(*p)--;` | - : Decrement byte at current pointer |
| 31 | `else if(s[i]=='.')write(1,p,1);` | . : Output byte at pointer |
| 32-39 | `else if(s[i]=='['&&!*p)` | [ : If current byte is zero, skip to matching ] |
| 33 | `depth=1;` | Depth starts at 1 (the current opening bracket) |
| 34-38 | `while(depth)` | Count forward through program to find matching ] |
| 35 | `i++;` | Advance to next character |
| 36 | `if(s[i]=='[')depth++;` | Nested [ increases depth needed to find matching ] |
| 37 | `if(s[i]==']')depth--;` | Matching ] found when depth reaches 0 |
| 40-47 | `else if(s[i]==']'&&*p)` | ] : If current byte is non-zero, jump back to matching [ |
| 41 | `depth=1;` | Depth starts at 1 (the current closing bracket) |
| 42-46 | `while(depth)` | Count backward through program to find matching [ |
| 43 | `i--;` | Move backward through program |
| 44 | `if(s[i]==']')depth++;` | Nested ] increases depth |
| 45 | `if(s[i]=='[')depth--;` | Matching [ found when depth reaches 0 |
| 48 | `i++;` | Advance to next instruction (for non-bracket chars, always advance) |

## Common Traps
- ❌ Nested loops (must count depth, not just find next bracket - for "[[]]", first ] matches first [)
- ❌ Pointer going past array bounds (no bounds checking - pointer can go before m or after m[2048])
- ❌ Not initializing array to 0 (all cells must start at 0 per Brainfuck spec)

## Related
- [[rpn_calc]] - stack-based parsing
- [[flood_fill]] - recursive algorithm
- EXAMS INDEX|Exam INDEX
