---
tags: [C02, flashcard]
creation_date: 2026-03-28
---


## ft_strcpy
Domanda::What does ft_strcpy do?
Risposta::Copies src string into dest, including \0. Returns dest.

## ft_strncpy  
Domanda::How does ft_strncpy differ from strcpy?
Risposta::Copies at most n chars. Pads with \0 if src < n. Returns dest.

## ft_str_is_alpha
Domanda::What does ft_str_is_alpha return?
Risposta::1 if all chars are letters (A-Z or a-z), else 0.

## ft_strupcase
Domanda::How convert to uppercase?
Risposta::If char between 'a' and 'z', subtract 32 (or use toupper)

## ft_strcapitalize
Domanda::What is word start condition?
Risposta::i==0 OR str[i-1] is NOT letter/digit

## ft_strlcpy
Domanda::Why better than strncpy?
Risposta::Guarantees null-termination, returns src length for truncation detection

## Pointer arithmetic
Domanda::What is *(p+i) equivalent to?
Risposta::p[i] - same thing!

## String literals
Domanda::Can you modify a string literal?
Risposta::NO - undefined behavior. String literals are read-only.
