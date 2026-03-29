---
tags: [flashcard]
date: 2026-03-29
status: complete
---
# Git for 42

---
tags:
  - [Manual, gray]
---

> ~={blue} Version control workflow =~

## Navigation
← [[C11_Index|Vault Home]]

## Basic Workflow
```bash
# Clone repository
git clone git@vogsphere.42.fr:...

# Check status
git status

# Add changes
git add .

# Commit
git commit -m "feat: description"

# Push
git push
```

## Commit Messages
- `feat:` - New feature
- `fix:` - Bug fix
- `refactor:` - Code cleanup
- `docs:` - Documentation

## Useful Commands
```bash
git log --oneline        # Compact log
git diff                 # Show changes
git checkout -- file     # Discard changes
git reset HEAD file      # Unstage file
```

How do you push to 42?
::
```bash
git add .
git commit -m "message"
git push
```

## Related
- Shell00/git_commit.sh|Git Commit Exercise
- Shell00/gitignore|Gitignore Exercise
