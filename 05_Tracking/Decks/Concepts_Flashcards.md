---
tags: [concepts, flashcard]
---


# Concepts Flashcards

Core programming concepts for 42 Piscine: memory, algorithms, and system calls.

---

## NULL Pointer

Why does dereferencing a NULL pointer crash?::La CPU non può accedere all'indirizzo ==0== (non valido o protetto)

What is segmentation fault?::Errore quando il programma tenta di accedere a memoria ==non autorizzata==

Cosa succede quando si dereferenzia NULL?::Il programma ==crasha== (Segmentation Fault)

---

## malloc

What does malloc return?::L'==indirizzo== del blocco di memoria allocata (o NULL se fallisce)

malloc alloca memoria dove?::Nello ==heap== (non nello stack)

Cosa devi sempre fare dopo malloc?::Controllare se il valore di ritorno è ==NULL==

---

## Stack vs Heap

Dove sono memorizzate le variabili locali?::Nello ==stack==

Dove viene allocata la memoria da malloc?::Nell'==heap==

Cosa significa "lo stack cresce verso il basso"?::Gli indirizzi diminuiscono quando aggiungi variabili locali

---

## Array Decay

What happens when you pass an array to a function?::Decade a ==puntatore== al primo elemento

Why can't you use sizeof on an array parameter?::Perché il parametro array è già ==decaduto== a puntatore

Cosa significa "array decay"?::Un array perde le sue dimensioni e diventa un ==puntatore== al primo elemento

---

## strncpy vs strlcpy

Why is strlcpy safer than strncpy?::==Garantisce la null terminazione== (se size > 0)

strncpy problem: What if src is shorter than n?::Non aggiunge il terminatore nullo

strlcpy: What does it always do?::Aggiunge sempre =='\0'== se size > 0

strlcpy: What does it return?::La ==lunghezza di src== (utile per detectare truncation)

---

## GCD Algorithm (Euclidean)

How do you calculate GCD(a, b)?::```
while (b != 0) {
    temp = b;
    b = a % b;
    a = temp;
}
```

GCD: Cosa fa `a % b`?::Restituisce il ==resto== della divisione a diviso b

Quante iterazioni servono per GCD(48, 18)?::3 (48%18=12, 18%12=6, 12%6=0 → GCD=6)

---

## Bubble Sort

How does bubble sort know when array is sorted?::Quando un ==passaggio completo== senza nessuno swap

Bubble sort: What causes reset to i=0 after swap?::Per controllare che elementi fuori posizione vengano spostati correttamente

Bubble sort: Worst case complexity?::O(n²) (ogni elemento confrontato con ogni altro)

---

## Recursion

What stops infinite recursion?::Il ==base case== (condizione di terminazione)

ft_putnbr: Why use recursion?::Per processare le cifre dalla ==più significativa== alla meno significativa

Cosa succede senza base case?::==Stack overflow== (chiamate infinite consumano tutta la memoria)

---

## int vs long long for INT_MIN

Why use long long for INT_MIN in ft_putnbr?::Negare ==INT_MIN== causa overflow (il valore assoluto è maggiore del massimo int positivo)

INT_MIN: What is it?::-2147483648 (32 bit) o -9223372036854775808 (64 bit)

Perché -(-2147483648) overflowa?::Il valore positivo ==2147483648== eccede INT_MAX (2147483647)

---

## write vs printf

Why is write considered lower level?::È una ==syscall==, non ha buffering, opera direttamente su file descriptor

What file descriptor is stdout?::1

printf vs write: What's the key difference?::printf ha ==buffering==, write no; printf è libreria, write è syscall

Cosa significa "syscall"?::Una ==richiesta al kernel== del sistema operativo per operazioni di basso livello
