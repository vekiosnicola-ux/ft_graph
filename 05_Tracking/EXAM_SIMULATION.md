---
tags: [exam, practice, simulation]
creation_date: <% tp.date.now() %>
exam_level: <% tp.system.prompt("Exam level (0-5)", "0") %>
duration_minutes: 30
---


# 🎯 Exam Simulation: Level `<% tp.system.prompt("Level", "0") %>`

**Date:** <% tp.date.now("YYYY-MM-DD") %>
**Duration:** <% tp.system.prompt("Duration (minutes)", "30") %> minutes
**Level:** <% tp.system.prompt("Level", "0") %>

---

## ⏱️ Timer
> Start: <% tp.date.now("HH:mm") %>
> End: <% tp.date.now("HH:mm", 0, 0, <% tp.system.prompt("Duration", "30") %>) %>

---

## 📋 Instructions
1. Set timer for <% tp.system.prompt("Duration", "30") %> minutes
2. Pick a random exercise from the level
3. Code it without looking at solutions
4. When time is up, reveal solution and self-grade

---

## 🎲 Random Exercise Selector

### Level 0 (1 point)
```dataview
LIST random("03_Exams/Level_0/*")
LIMIT 1
```

### Level 1 (2 points)
```dataview
LIST random("03_Exams/Level_1/*")
LIMIT 1
```

### Level 2 (3 points)
```dataview
LIST random("03_Exams/Level_2/*")
LIMIT 1
```

---

## 📊 Self-Grading

| Criteria | Score (0-5) |
|----------|------------|
| Compiles with -Wall -Wextra -Werror | /5 |
| Norminette compliance | /5 |
| Correct output | /5 |
| Edge cases handled | /5 |

**Total:** ___/20

---

## 🔄 Review Plan
- If score < 15: Review concept: concept_link
- If score < 10: Redo exercise tomorrow
- If score > 15: Add to spaced repetition deck

---

## 💡 Post-Exam Reflection
What went well?
-

What was difficult?
-

What to review?
-

---

## 📚 Related Concepts
```dataview
LIST file.link
FROM "01_Concepts"
WHERE contains(file.name, <% tp.system.prompt("Topic", "pointers") %>)
LIMIT 5
```
