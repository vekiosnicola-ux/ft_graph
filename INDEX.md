---
tags: [Dashboard, Vault]
date: 2026-03-29
status: complete
---


# 🌌 42 Piscine Knowledge Vault

Welcome to the central hub. All modules, concepts, and references are accessible from here.

---

## 📚 Active Modules

```dataview
TABLE status, date AS "Last Updated"
FROM "02_Modules"
WHERE file.name != "INDEX"
SORT file.mtime DESC
LIMIT 10
```

---

## 🧠 Core Concepts & CheatSheets

```dataview
TABLE status AS "Status"
FROM "01_Concepts" OR "05_Tracking"
WHERE file.name != "INDEX"
SORT file.name ASC
```

---

## 🛠️ Tools & Snippets

```dataview
TABLE length(file.inlinks) AS "References"
FROM "07_Manual"
WHERE file.name != "INDEX"
SORT file.mtime DESC
LIMIT 5
```

---

## 🚀 Projects & Challenges

```dataview
LIST
FROM "04_Projects"
WHERE file.name != "INDEX"
SORT file.name ASC
```

---

## 🎯 Exams Focus

```dataview
TABLE status AS "Status", tags AS "Tags"
FROM "03_Exams"
WHERE file.name != "INDEX"
SORT file.name ASC
LIMIT 10
```

## 🕸️ Vault Architecture (Graph Links)
- [[00_CONTROL_Index|00_CONTROL]]
- [[01_Concepts_Index|01_Concepts]]
- [[Tutorials_Index|Tutorials]]
- [[C00_Index|C00]]
- [[C01_Index|C01]]
- [[C02_Index|C02]]
- [[C03_Index|C03]]
- [[C04_Index|C04]]
- [[C05_Index|C05]]
- [[C06_Index|C06]]
- [[C07_Index|C07]]
- [[C08_Index|C08]]
- [[C09_Index|C09]]
- [[C10_Index|C10]]
- [[C11_Index|C11]]
- [[C12_Index|C12]]
- [[C13_Index|C13]]
- [[Shell00_Index|Shell00]]
- [[Shell01_Index|Shell01]]
- [[03_Exams_Index|03_Exams]]
- [[Level_0_Index|Level_0]]
- [[Level_1_Index|Level_1]]
- [[Level_2_Index|Level_2]]
- [[Level_3_Index|Level_3]]
- [[Level_4_Index|Level_4]]
- [[Level_5_Index|Level_5]]
- [[chall00_Index|chall00]]
- [[chall01_Index|chall01]]
- [[chall02_Index|chall02]]
- [[Rush00_Index|Rush00]]
- [[Rush01_Index|Rush01]]
- [[Rush02_Index|Rush02]]
- [[Decks_Index|Decks]]
- [[05_Tracking_Index|05_Tracking]]
- [[07_Manual_Index|07_Manual]]
- [[Snippets_Index|Snippets]]
