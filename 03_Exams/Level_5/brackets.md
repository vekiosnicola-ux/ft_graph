---
tags: [Level_5, exam]
  - stack
  - parsing
  - white
---


# brackets

## What it does
Checks if brackets (), [], {} are balanced and properly nested. Prints "OK\n" or "Error\n"

## The Insight
Stack-based algorithm. Push on open brackets, pop on close brackets, check matching pairs.

## Step-by-step Algorithm
1. char stack[4096]; int top=0
2. Loop through string: if open bracket, stack[top++]=it
3. If close: if top==0 return Error; pop and check if matches (')' needs '(', etc.); if mismatch return Error
4. Ignore non-bracket chars
5. At end: if top==0 return OK, else Error

## The Code
```c
// brackets: Checks if bracket characters are balanced and properly nested
// Valid pairs: ()  []  {}
// Properly nested: ( [ ] ) - valid, ( [ ) ] - invalid
// Input: arbitrary string, Output: "OK\n" or "Error\n"

int check_brackets(char *s){
    char stack[4096];                      // Stack array to hold opening brackets
    int top=0;                            // Stack pointer: index of next empty slot
    int i=0;                               // Input string index
    
    while(s[i]){                          // Loop through each character in string
        if(s[i]=='('||s[i]=='['||s[i]=='{')  // If opening bracket
            stack[top++]=s[i];             // Push onto stack, increment top
        else if(s[i]==')'||s[i]==']'||s[i]=='}'){  // If closing bracket
            if(top==0)                     // Stack empty = no matching opening bracket
                return 0;                   // Error: unmatched closing bracket
            top--;                         // Pop: decrement top to get opening bracket
            if((s[i]==')'&&stack[top]!='(')||  // Check if brackets match
               (s[i]==']'&&stack[top]!='[')||
               (s[i]=='}'&&stack[top]!='{')){
                return 0;                   // Error: mismatched bracket types
            }
        }
        i++;                                // Move to next character (ignore non-bracket chars)
    }
    return top==0;                         // At end: if stack empty = OK, else = unclosed brackets
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 22 | `int check_brackets(char *s)` | Returns 1 for balanced/OK, 0 for Error |
| 23 | `char stack[4096];` | Stack array to store opening brackets as they're encountered |
| 24 | `int top=0;` | Stack pointer: index of next empty slot (also = count of items) |
| 25 | `int i=0;` | Input string index |
| 26 | `while(s[i])` | Loop through each character of input string |
| 27-28 | `if(s[i]=='('||s[i]=='['||s[i]=='{')` | If current char is an opening bracket |
| 28 | `stack[top++]=s[i];` | Push onto stack, increment top to mark next slot |
| 29-37 | `else if(s[i]==')'||s[i]==']'||s[i]=='}')` | If current char is closing bracket |
| 30 | `if(top==0)` | Stack empty means no opening bracket to match |
| 31 | `return 0;` | Error: unmatched closing bracket |
| 32 | `top--;` | Pop: move to previous stack position (get the opening bracket) |
| 33-36 | `if((s[i]==')'&&stack[top]!='(')||...)` | Check if popped bracket matches current closing bracket |
| 38 | `i++;` | Non-bracket characters are ignored, just advance to next char |
| 40 | `return top==0;` | At end: top==0 means all brackets matched (return 1), else unclosed (return 0) |

## Common Traps
- ❌ Popping empty stack (check top==0 before popping - forgetting this causes stack underflow)
- ❌ Not checking final stack is empty (at end, stack must be empty for valid string)
- ❌ Mismatched bracket types ('(' doesn't match '[' - must check exact pair)
- ❌ Nested loops (depth counting handles nested brackets correctly via stack)

## Related
- [[rpn_calc]] - stack-based calculator
- [[brainfuck]] - interpreter pattern
- EXAMS INDEX|Exam INDEX
