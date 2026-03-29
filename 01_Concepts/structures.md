---
tags: [Concepts]
---


# Structures (struct)

## What It Is
A struct is a composite data type that groups together variables (members) under a single name. Unlike arrays, struct members can be of different types. Structures enable creation of custom data types to represent complex objects like points, employees, or any real-world entity with multiple attributes.

## Key Points
- Define with `struct StructName { members };`
- Access members with `.` operator (or `->` for pointers to structs)
- Members are stored sequentially in memory (padding may occur for alignment)
- Can contain arrays, other structs, pointers
- Use `typedef` to create alias for cleaner syntax
- Pass structs by value (copied) or by pointer (efficient for large structs)

## Related Concepts
- [[pointers]]
- typedef
- [[linked_lists]]

## Examples
```c
// Basic struct definition
struct Point {
    int x;
    int y;
};

// Using typedef for cleaner syntax
typedef struct {
    char name[50];
    int age;
    float gpa;
} Student;

// Creating and initializing
struct Point p1 = {10, 20};      // designated initializer
struct Point p2 = {.x = 5, .y = 15};
Student s1 = {"Alice", 20, 3.75};

// Accessing members
p1.x = 30;
s1.gpa = 3.9;

// Struct as function parameter (passed by value - full copy)
float calc_distance(struct Point a, struct Point b) {
    int dx = a.x - b.x;
    int dy = a.y - b.y;
    return sqrt(dx*dx + dy*dy);
}

// Struct pointer (passed by reference - no copy)
void init_point(struct Point *p, int x, int y) {
    p->x = x;    // same as (*p).x but cleaner
    p->y = y;
}

// Array of structs
struct Point path[100];
for (int i = 0; i < 100; i++) {
    path[i].x = i;
    path[i].y = i * 2;
}
```

## Common Mistakes
- ❌ Forgetting to use `&` when passing struct to function expecting pointer
- ❌ Using `.` on struct pointer instead of `->`
- ❌ Comparing structs with `==` (compares memory, not member values)
- ❌ Returning local struct by value (OK for small structs, but careful with stack)
