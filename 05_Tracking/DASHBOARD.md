---
tags: [dashboard, tracking]
creation_date: 2026-03-28
---


## 🎯 42 Piscine Progress Dashboard

### Module Completion
```dataview
TABLE rows.file.name as "Exercise", module, status
FROM "02_Modules"
WHERE module
GROUP BY module
```

### Exercises by Status
```dataview
TABLE status, count
WHERE status
GROUP BY status
```

### Spaced Repetition Due
```dataview
TABLE file.ctime as "Last Review", file.mtime as "Next Due"
FROM "05_Tracking/Decks"
WHERE file.mtime < date(today)
SORT file.mtime ASC
```

### Weakest Areas (Files with Most Links)
```dataview
TABLE length(file.outlinks) as "Links", file.mtime as "Modified"
FROM "02_Modules"
WHERE length(file.outlinks) > 0
SORT length(file.outlinks) ASC
LIMIT 5
```

### Exam Readiness (C00-C04)
```dataview
TABLE rows.file.name as "Exercise"
FROM "03_Exams/Level_1"
FLATTEN "■□□□□" as status
WHERE status = "■□□□□"
```

### Quick Stats
- Total Files: `=length(list("02_Modules/*"))`
- C Modules: `=length(list("02_Modules/C*"))`
- Shell Modules: `=length(list("02_Modules/Shell*"))`
- Exam Exercises: `=length(list("03_Exams/**"))`

### Recent Reviews
```dataview
LIST file.mtime
FROM "05_Tracking/Decks"
SORT file.mtime DESC
LIMIT 5
```

### Links to Key Sections
- C00/INDEX|C00 Module
- C01/INDEX|C01 Module
- EXAMS INDEX|Exams
- 05_Tracking/FLASHCARDS_INDEX|Flashcards
- 05_Tracking/SPACED_REPETITION|Spaced Repetition Guide
