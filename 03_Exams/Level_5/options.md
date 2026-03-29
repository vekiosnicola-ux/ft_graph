---
tags: [Level_5, exam]
  - bitwise
  - argv
  - white
---


# options

## What it does
Parses command line options like "-abc" and prints 32-bit representation. Each bit = letter position.

## The Insight
Bit manipulation. flags |= (1 << (char - 'a')). Each bit in output represents whether that letter was set.

## Step-by-step Algorithm
1. flags=0
2. For each argv starting with '-': for each char, if lowercase letter, set bit: flags |= 1 << (c - 'a')
3. Print bits from 31 to 0

## The Code
```c
// options: Parses command-line options and displays as 32-bit binary
// Example: ./prog -abc sets bits 0,1,2 -> outputs 0000000000000000000000000111
// Each lowercase letter 'a'-'z' corresponds to bit position 0-25

int main(int ac,char**av){
    int flags=0;                           // 32-bit integer to store which options were set
    int i=1,j;                              // i=argv index, j=character index within arg
    
    while(i<ac){                            // Loop through each argument (skip argv[0] = program name)
        j=1;                                // Start at second character of arg (skip leading '-')
        while(av[i][j]){                    // Loop through characters of current argument
            if(av[i][j]>='a'&&av[i][j]<='z')  // If lowercase letter
                flags|=1<<(av[i][j]-'a');   // Set corresponding bit: 'a'->bit0, 'b'->bit1, etc.
            j++;                            // Move to next character in argument
        }
        i++;                                // Move to next argument
    }
    i=31;                                   // Start from most significant bit (bit 31)
    while(i>=0){                            // Print all 32 bits from MSB to LSB
        write(1,flags&(1<<i)?"1":"0",1);   // If bit i is set, print '1', else print '0'
        i--;                                // Move to next bit (going downward)
    }
    write(1,"\n",1);                        // Print newline at end
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 20 | `int main(int ac,char**av)` | Main function: ac=arg count, av=argument vector |
| 21 | `int flags=0;` | flags: 32-bit integer to store which option letters were found |
| 22 | `int i=1,j;` | i=which argument (skip av[0]=program name), j=character index |
| 23 | `while(i<ac)` | Loop through all arguments |
| 24 | `j=1;` | Start at second character of argument (skip the '-' prefix) |
| 25 | `while(av[i][j])` | Loop through characters in current argument (until null terminator) |
| 26 | `if(av[i][j]>='a'&&av[i][j]<='z')` | Check if character is lowercase letter |
| 27 | `flags\|=1<<(av[i][j]-'a');` | Set bit: 'a'-'a'=0 so 1<<0=1, 'b'-'a'=1 so 1<<1=2, etc. |
| 28 | `j++;` | Move to next character in argument |
| 30 | `i++;` | Move to next argument |
| 32 | `i=31;` | Start printing from bit 31 (most significant bit) |
| 33 | `while(i>=0)` | Loop while bits remain (down to bit 0) |
| 34 | `write(1,flags&(1<<i)?"1":"0",1);` | Check if bit i is set: if yes print '1', else print '0' |
| 35 | `i--;` | Move to next lower bit |
| 37 | `write(1,"\n",1);` | Print newline after binary output |

## Common Traps
- ❌ Wrong bit position calculation (must subtract 'a' to get correct bit position: 'c' - 'a' = 2 = bit 2)
- ❌ Not iterating correctly through argv (start at i=1 to skip program name)
- ❌ Printing in wrong direction (must print from bit 31 down to bit 0)

## Related
- [[print_memory]] - hex dump
- [[brainfuck]] - byte manipulation
- EXAMS INDEX|Exam INDEX
