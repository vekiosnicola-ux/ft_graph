---
tags: [Shell, flashcard]
---


## git add
Domanda::What does git add . do?
Risposta::Stages all changes in current directory for commit

## git commit
Domanda::What creates local commit history?
Risposta::git commit -m "message"

## chmod permissions
Domanda::What does chmod 755 do?
Risposta::Owner: rwx, Group: r-x, Others: r-x

## tar create
Domanda::How create tar archive?
Risposta::tar -cf archive.tar files/

## find -delete
Domanda::How delete files with find?
Risposta::find . -type f -name '*~' -delete

## ls flags
Domanda::What does ls -la show?
Risposta::Long format, all files (including hidden)

## SSH key generation
Domanda::How generate RSA SSH key?
Risposta::ssh-keygen -t rsa -b 4096 -C "email"

## git ls-files
Domanda::How list ignored files?
Risposta::git ls-files --ignored --exclude-standard
