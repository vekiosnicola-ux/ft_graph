---
tags: [exam, flashcard]
---


## Common Exam Error
Domanda::Why does write(1, c, 1) crash?
Risposta::c is a VALUE (like 97), write expects ADDRESS (&c)

## INT_MIN overflow
Domanda::Why use long long in ft_putnbr?
Risposta::Negating INT_MIN overflows int (range is asymmetric)

## Memory Layout
Domanda::Where does malloc allocate?
Risposta::Heap (vs stack for local variables)

## Array as Parameter
Domanda::What happens when array passed to function?
Risposta::Decays to pointer to first element

## Bubble Sort
Domanda::When is bubble sort complete?
Risposta::When a full pass occurs with no swaps

## GCD Algorithm
Domanda::Euclidean algorithm for GCD(a,b)?
Risposta::while(b != 0) { temp = b; b = a % b; a = temp; }

## Recursion Base Case
Domanda::Why need base case in recursion?
Risposta::Without it, infinite recursion (stack overflow)

## fizzbuzz 15
Domanda::What does fizzbuzz print for 15?
Risposta::fizzbuzz (divisible by both 3 AND 5)
