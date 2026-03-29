---
tags: [C03, flashcard]
---


## ft_strcmp
Domanda::What does ft_strcmp return when strings equal?
Risposta::0 (difference of two null terminators)

## ft_strncmp
Domanda::How many chars does ft_strncmp compare?
Risposta::At most n characters

## ft_strcat
Domanda::What does ft_strcat do?
Risposta::Appends src string to dest (after dest's \0). Returns dest.

## ft_strncat
Domanda::How does ft_strncat limit copies?
Risposta::Copies at most n chars from src, adds \0 at end

## ft_strstr
Domanda::What does ft_strstr find?
Risposta::First occurrence of substring needle in haystack, or NULL

## ft_strlcat
Domanda::What does ft_strlcat return?
Risposta::Total length of dest + src (intended length)

## Concatenation gotcha
Domanda::Why must dest have enough space?
Risposta::Otherwise buffer overflow - undefined behavior

## String search
Domanda::How traverse to find substring?
Risposta::Nested loops - outer for haystack, inner for needle match
