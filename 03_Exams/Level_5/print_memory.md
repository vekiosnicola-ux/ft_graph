---
tags: [Level_5, exam]
  - memory
  - hex
  - white
---


# print_memory

## What it does
Prints hex dump of memory like hexdump. For each 16-byte chunk: address | hex bytes | ascii chars.

## The Insight
Cast void* to unsigned char*. Outer loop 16 bytes at a time. Inner loops: first print hex (with padding for partial last line), second print ascii (printable or '.').

## Step-by-step Algorithm
1. Cast to unsigned char*
2. Loop while remaining >= 16: print 16 hex bytes, print 16 ascii chars
3. Handle partial final line: print hex with spaces for missing, print ascii for present bytes

## The Code
```c
// print_memory: Prints hex dump of memory contents
// Format per line: [address] [hex bytes...] [ascii representation]
// Example: 16 bytes per line, hex values space-separated, ascii shows printable chars or '.'

void print_memory(const void *addr, size_t size){
    const unsigned char *p=addr;           // Cast void* to unsigned char* for byte access
    size_t i=0;                            // Current position in memory
    
    while(i<size){                         // Process 16 bytes at a time
        int j=0;                           // j counts actual bytes in this chunk (up to 16)
        while(j<16&&i+j<size)              // Count how many bytes in this chunk (1-16)
            j++;                           // j = min(16, remaining bytes)
        int k=0;                           // k = index within this chunk
        while(k<j){                         // Print hex representation
            unsigned char c=p[i+k];         // Get byte at position i+k
            char hex[3];                   // Two hex chars + null terminator
            hex[0]=c/16<10?'0'+c/16:'a'+c/16-10;  // High nibble: 0-9 -> '0'-'9', 10-15 -> 'a'-'f'
            hex[1]=c%16<10?'0'+c%16:'a'+c%16-10;   // Low nibble: same mapping
            hex[2]=0;                       // Null terminate string
            write(1,hex,2);                 // Write two hex digits
            if(k<15)                       // Space between bytes, except after last
                write(1," ",1);
            k++;
        }
        while(k<16){                       // Pad hex column if partial line (less than 16 bytes)
            write(1,"   ",3);              // Three spaces for each missing byte
            k++;
        }
        k=0;                               // Reset k for ASCII output
        write(1," ",1);                     // Space between hex and ASCII columns
        while(k<j){                         // Print ASCII representation
            if(p[i+k]>=32&&p[i+k]<127)      // If printable ASCII (space through tilde)
                write(1,&p[i+k],1);         // Print character directly
            else
                write(1,".",1);             // Print '.' for non-printable bytes
            k++;
        }
        write(1,"\n",1);                    // Newline after each line
        i+=16;                              // Move to next 16-byte chunk
    }
}
```

## Line-by-Line Translation
| Line | Code | Translation |
|------|------|------------|
| 20 | `void print_memory(const void *addr, size_t size)` | Takes memory address and number of bytes to display |
| 21 | `const unsigned char *p=addr;` | Cast void pointer to byte-accessible pointer |
| 22 | `size_t i=0;` | i = current position (size_t for large sizes) |
| 23 | `while(i<size)` | Outer loop: process until all bytes printed |
| 24 | `int j=0;` | j = number of valid bytes in current chunk |
| 25-26 | `while(j<16&&i+j<size)` | Count bytes: up to 16, but stop at end of data |
| 27 | `int k=0;` | k = index within current chunk for hex output |
| 28-38 | `while(k<j)` | Print hex column: print j bytes as hex |
| 30 | `unsigned char c=p[i+k];` | Get current byte value |
| 31 | `hex[0]=c/16<10?...` | High nibble (first hex digit): c/16 gives 0-15 |
| 32 | `hex[1]=c%16<10?...` | Low nibble (second hex digit): c%16 gives 0-15 |
| 36-37 | `if(k<15) write(1," ",1);` | Add space after each hex byte except last in line |
| 39-42 | `while(k<16)` | Pad remaining space if less than 16 bytes |
| 43 | `write(1," ",1);` | Space between hex column and ASCII column |
| 44 | `int k=0;` | Reset k=0 for ASCII column |
| 45-50 | `while(k<j)` | Print ASCII column: j bytes |
| 47-48 | `if(p[i+k]>=32&&p[i+k]<127)` | Check if printable ASCII (space is printable) |
| 49 | `write(1,&p[i+k],1);` | Print character directly |
| 50 | `write(1,".",1);` | Non-printable: show '.' placeholder |
| 51 | `write(1,"\n",1);` | End of line: newline |
| 52 | `i+=16;` | Advance to next 16-byte block |

## Common Traps
- ❌ Partial final line padding (hex column misaligns without proper spaces - must print 3 spaces per missing byte)
- ❌ Non-printable chars (must show '.' for bytes outside 32-126 range)
- ❌ Wrong hex conversion (nibble calculation must use integer division and modulo)

## Related
- [[ft_itoa_base]] - hex conversion
- [[options]] - bit manipulation
- EXAMS INDEX|Exam INDEX
