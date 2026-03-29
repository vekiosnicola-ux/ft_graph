---
tags: []
date: 2026-03-29
status: complete
---
# Progress Dashboard

---
tags: [Tracking, brown]
---

## Navigation
← [[C11_Index|Back to Home]] | 05_Tracking/INDEX|Tracking INDEX

## Overview
```dataview
TABLE length(rows) as "Exercise Count"
FROM "02_Modules"
GROUP BY file.folder as Module
SORT Module ASC
```

## Mastery Status
```dataview
TABLE
  choice(mastery = "□□□□□", "🆕 New",
    choice(mastery = "■□□□□", "📚 Developing",
      choice(mastery = "■■□□□", "✅ Competent",
        choice(mastery = "■■■□□", "⭐ Proficient",
          choice(mastery = "■■■■■", "🏆 Master", mastery))))) as Status
FROM "02_Modules"
SORT file.folder ASC, file.name ASC
```

## Recent Activity
```dataview
TABLE last-review as "Last Review", next-due as "Next Due"
FROM "02_Modules"
WHERE last-review
SORT last-review DESC
LIMIT 10
```

## Study Streak
- **Current Streak:** 0 days
- **Longest Streak:** 0 days
- **Total Study Days:** 0

## Module Progress
| Module | Total | New | Developing | Competent | Proficient | Master |
|--------|-------|-----|------------|-----------|------------|--------|
| Shell00 | 10 | 10 | 0 | 0 | 0 | 0 |
| Shell01 | 8 | 8 | 0 | 0 | 0 | 0 |
| C00 | 9 | 9 | 0 | 0 | 0 | 0 |
| C01 | 9 | 9 | 0 | 0 | 0 | 0 |
| C02 | 13 | 13 | 0 | 0 | 0 | 0 |
| C03 | 6 | 6 | 0 | 0 | 0 | 0 |
| C04 | 8 | 8 | 0 | 0 | 0 | 0 |
| C05 | 11 | 11 | 0 | 0 | 0 | 0 |
| C06 | 11 | 11 | 0 | 0 | 0 | 0 |
| C07 | 9 | 9 | 0 | 0 | 0 | 0 |
| C08 | 6 | 6 | 0 | 0 | 0 | 0 |
| C09 | 3 | 3 | 0 | 0 | 0 | 0 |
| C10 | 4 | 4 | 0 | 0 | 0 | 0 |
| C11 | 9 | 9 | 0 | 0 | 0 | 0 |
| C12 | 10 | 10 | 0 | 0 | 0 | 0 |
| C13 | 9 | 9 | 0 | 0 | 0 | 0 |

## Exam Readiness
```dataview
TABLE
  choice(file.folder = "03_Exams/Level_0", "Level 0",
    choice(file.folder = "03_Exams/Level_1", "Level 1",
      choice(file.folder = "03_Exams/Level_2", "Level 2",
        choice(file.folder = "03_Exams/Level_3", "Level 3",
          choice(file.folder = "03_Exams/Level_4", "Level 4",
            choice(file.folder = "03_Exams/Level_5", "Level 5", "Unknown")))))) as Level
FROM "03_Exams"
SORT file.folder ASC, file.name ASC
```
