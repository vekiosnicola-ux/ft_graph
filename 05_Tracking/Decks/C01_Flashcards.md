---
tags: [C01, flashcard]
---


# C01 Flashcards

Pointers, swap functions, and array manipulation from 42 Piscine C01.

---

## ft_ft

What does `ft_ft(int *nbr)` do?::Imposta il valore puntato da nbr a ==42==

Quanti livelli di puntatore in ft_ultimate_ft?::9 (==int *********nbr==)

---

## ft_swap

Why does ft_swap need pointers?::Per modificare le variabili **originali** (C passa parametri per valore)

ft_swap: What is the algorithm?::Usa una variabile temp per non perdere un valore durante lo swap

```
temp = *a;
*a = *b;
*b = temp;
```

---

## ft_div_mod

What do the `div` and `mod` pointers store after calling ft_div_mod?::`div` memorizza ==quoziente== (a/b), `mod` memorizza ==resto== (a%b)

ft_div_mod: Why check `b != 0`?::Per evitare ==divisione per zero== (undefined behavior)

---

## ft_ultimate_ft

Quanti asterischi ci sono in `int *********nbr`?::9 (nove livelli di puntatore)

ft_ultimate_ft: How do you reach the final integer?::Dereferenziando tutti e nove i livelli: `*********nbr = 42`

---

## ft_strlen

What stops the while loop in ft_strlen?::Il ==null terminator== (`'\0'`)

ft_strlen returns what?::Il ==numero di caratteri== prima del terminatore nullo

---

## ft_rev_int_tab

How does ft_rev_int_tab reverse an array in place?::Swappa l'elemento all'inizio con quello alla fine, poi muove ==verso il centro==

What indices are used?::`start = 0`, `end = size - 1`, e scambia mentre `start < end`

---

## ft_sort_int_tab

What sorting algorithm does ft_sort_int_tab use?::==Bubble sort== con reset dell'indice dopo ogni swap

ft_sort_int_tab: When is sorting complete?::Quando un intero passaggio completo senza nessuno ==swap==

ft_sort_int_tab: Why reset i to 0 after a swap?::Per assicurarsi che elementi non ordinati vengano controllati dall'inizio

---

## Memory: int vs char

How many bytes does a `char` typically use?::1 byte

How many bytes does an `int` typically use?::4 bytes (32 bit)

What is array decay?::Quando un array viene passato a una funzione, decade a ==puntatore== al primo elemento

---

## ft_ultimate_div_mod

What does ft_ultimate_div_mod do?::Esegue divisione E modulo, memorizzando entrambi i risultati nelle variabili originali via puntatori

ft_ultimate_div_mod: Why store original *a before overwriting?::Perché `*a = *a / *b` perderebbe il valore originale necessario per calcolare il resto
