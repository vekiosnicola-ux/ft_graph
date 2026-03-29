---
tags: [C00, flashcard]
---


# C00 Flashcards

Basic C functions, loops, and alphabet patterns from 42 Piscine C00.

---

## ft_putchar

What function outputs a single character to stdout?::`write(1, &c, 1)`

La funzione ft_putchar usa la syscall ==write(1, &c, 1)== per output

---

## ft_print_alphabet

What loop prints a-z?::`while(letter <= 'z')` with `letter++`

ft_print_alphabet uses what start and end values?::Start at `'a'`, end at `'z'`

---

## ft_is_negative

What does ft_is_negative print for a negative number?::`'N'`

What does ft_is_negative print for a positive number?::`'P'`

---

## fizzbuzz

What does fizzbuzz print for 15?::`fizzbuzz` (multiplo di 3 AND 5)

fizzbuzz: when does it print "fizz"?::Quando il numero è divisibile per ==3==

fizzbuzz: when does it print "buzz"?::Quando il numero è divisibile per ==5==

---

## ft_putnbr

How does ft_putnbr handle negative numbers?::Stampa `'-'` poi converte a positivo con `long long`

ft_putnbr: Why use long long?::Per evitare overflow con ==INT_MIN== quando si nega

ft_putnbr: Why recursion?::Per stampare le cifre nell'ordine corretto (la prima cifra processata per ultima)

---

## ft_print_comb

How does ft_print_comb prevent trailing comma?::Check if `!(i == '7' && j == '8' && k == '9')` prima di stampare `", "`

ft_print_comb: Why nested loops ensure uniqueness?::Perché ogni cifra è sempre maggiore della precedente: ==i < j < k==

---

## ASCII Values

Qual è il valore ASCII di 'A'?::65

Qual è il valore ASCII di 'a'?::97

Qual è il valore ASCII di '0'?::48

What is the difference 'A' - 'a'?::-32 (uppercase are 32 positions lower in ASCII)

---

## Pointers Basics

What does `*p = 42` do?::Cambia il **valore** all'indirizzo contenuto in p

What does `p = &x` do?::Cambia **dove** punta p, memorizzando l'indirizzo di x

What does `&x` return?::L'indirizzo di memoria della variabile x

---

## write syscall

Why does `write(1, &c, 1)` work but `write(1, c, 1)` crashes?::write richiede un **indirizzo**. Passando c passa il valore ASCII (es. 97), e l'OS tenta di leggere dall'indirizzo 97

Cosa richiede il secondo parametro di write?::Un ==indirizzo di memoria== da cui leggere

---

## ft_print_reverse_alphabet

What is the loop condition for ft_print_reverse_alphabet?::`while (letter >= 'a')`

Why does decrementing a char work for reverse alphabet?::I caratteri in C sono rappresentati come ==interi ASCII==, quindi decrementare muove attraverso l'alfabeto
