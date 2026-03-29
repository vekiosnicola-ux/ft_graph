---
tags: [Level_5, exam]
  - stack
  - calculator
  - white
---


# rpn_calc

## What it does
Reverse Polish Notation calculator. "3 4 +" = 7. Operators: + - * / %

## The Insight
Stack-based. Numbers push, operators pop two, compute, push result.

## Step-by-step Algorithm
1. stack[4096], top=0
2. Parse string: if digit, atoi (handle multi-digit), push
3. If operator: pop b=stack[--top], pop a=stack[--top], compute a op b, push result
4. Division by zero = Error
5. At end: print stack[0]

## The Code
```c
// rpn_calc: Reverse Polish Notation calculator
// Input format: "3 4 +" (spaces between tokens)
// Operators: + - * / %
// Handles multi-digit numbers

void rpn_calc(char *s){
    int stack[4096];                      // Stack array: holds operands
    int top=0;                            // Stack pointer: index of next empty slot
    int i=0;                              // Input string index
    
    while(s[i]){                          // Parse input string character by character
        if(s[i]>='0'&&s[i]<='9'){         // If current char is a digit
            int n=0;                       // Build multi-digit number
            while(s[i]>='0'&&s[i]<='9'){   // While still reading digits
                n=n*10+s[i]-'0';           // Accumulate: shift previous digits left, add new digit
                i++;                       // Move to next character
            }
            stack[top++]=n;                // Push number onto stack, increment top
        }
        else if(s[i]=='+'||s[i]=='-'||s[i]=='*'||s[i]=='/'||s[i]=='%'){  // If operator
            if(top<2){                     // Need at least 2 operands for operator
                write(1,"Error\n",6);     // Error: not enough operands
                return;
            }
            int b=stack[--top];            // Pop second operand (b = stack[--top])
            int a=stack[--top];            // Pop first operand (a = stack[--top])
            int r;                         // Result variable
            if(s[i]=='+')r=a+b;           // Addition
            else if(s[i]=='-')r=a-b;       // Subtraction
            else if(s[i]=='*')r=a*b;       // Multiplication
            else if(s[i]=='/'){             // Division
                if(b==0){                   // Check for division by zero
                    write(1,"Error\n",6);  // Error: division by zero
                    return;
                }
                r=a/b;                     // Integer division
            }
            else r=a%b;                    // Modulo
            stack[top++]=r;                // Push result back onto stack
        }
        i++;                                // Move to next character (skip spaces and non-operator chars)
    }
    putnbr(stack[0]);                      // After processing, result is at stack[0]
    write(1,"\n",1);                       // Print newline
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 22 | `void rpn_calc(char *s)` | RPN calculator: takes string input |
| 23 | `int stack[4096];` | Stack array to hold operands (large enough for any input) |
| 24 | `int top=0;` | Stack pointer: points to next empty position (also = number of items) |
| 25 | `int i=0;` | Input string index |
| 26 | `while(s[i])` | Main parsing loop: while not end of string |
| 27 | `if(s[i]>='0'&&s[i]<='9')` | Check if current char is digit |
| 28 | `int n=0;` | Number accumulator for multi-digit numbers |
| 29-32 | `while(s[i]>='0'&&s[i]<='9')` | Build complete number (handles "123" as single token) |
| 30 | `n=n*10+s[i]-'0';` | Accumulate: n = n*10 + numeric value of digit |
| 31 | `i++;` | Advance through consecutive digits |
| 33 | `stack[top++]=n;` | Push number onto stack (post-increment top) |
| 35-55 | `else if(s[i]=='+'\|\|...` | If operator character found |
| 36-38 | `if(top<2)` | Check: need 2 operands for binary operator |
| 40 | `int b=stack[--top];` | Pop second operand: decrement top THEN use value |
| 41 | `int a=stack[--top];` | Pop first operand: same pattern |
| 43-52 | `if(s[i]=='+')...else if...` | Compute result based on operator |
| 47-50 | `else if(s[i]=='/')` | Division: check b != 0 first |
| 54 | `stack[top++]=r;` | Push computed result back onto stack |
| 56 | `i++;` | Skip non-digit, non-operator characters (spaces) |
| 58 | `putnbr(stack[0]);` | Final result is at bottom of stack (stack[0]) |
| 59 | `write(1,"\n",1);` | Print newline after result |

## Common Traps
- ❌ Order of operands in division/subtraction (a op b, NOT b op a - for "3 4 -" result is -1: a=3, b=4, so a-b = -1)
- ❌ Division by zero (check b == 0 before dividing)
- ❌ Stack underflow (top < 2 check ensures we have enough operands)

## Related
- [[brackets]] - stack parsing
- [[brainfuck]] - interpreter pattern
- EXAMS INDEX|Exam INDEX
