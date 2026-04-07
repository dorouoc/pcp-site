---
id: Dashboard-Research-Progress
title: "📊 Dashboard — Research Progress"
type: dashboard
tags: [dashboard, research, progress, puma, dataview]
created: 2026-03-01
updated: 2026-04-06
---

# 📊 Dashboard — Research Progress

---

## Literature Pipeline

```dataview
TABLE WITHOUT ID length(rows) AS "Count", rows.file.link AS "Papers"
FROM #literature
GROUP BY status
SORT status ASC
```

---

## Reading Queue (Pass 1 needed)

```dataview
TABLE title AS "Title", first-author AS "Author", year AS "Year", relevance AS "⭐"
FROM #literature
WHERE status = "to-read"
SORT relevance DESC
LIMIT 10
```

---

## High-Priority Papers Not Yet Reviewed

```dataview
TABLE title AS "Title", first-author AS "Author", year AS "Year", topic AS "Topic"
FROM #literature
WHERE relevance >= 4 AND status != "reviewed"
SORT relevance DESC
```

---

## Writing Progress

```dataview
TABLE status AS "Status", file.mtime AS "Last Modified"
FROM "40 - Projects/PUMA"
WHERE type = "project-note"
SORT file.mtime DESC
```

---

## Chapter Completion Tracker

| Chapter | Status | Word Target | Notes |
|---------|--------|-------------|-------|
| Ch.1 Introduction | ✅ Complete | ~4,000 | delivered |
| Ch.2 Materials & Methods | 🔄 In progress | ~3,000 | Methods design complete |
| Ch.3 Results | ⏳ Pending experiments | ~2,500 | Awaiting PEC2 data |
| Ch.4 Conclusions | ⏳ Pending | ~1,500 | After results |
| Ch.5 Glossary | 🔄 Ongoing | — | 65 terms in vault |
| Ch.6 Bibliography | ✅ 42 refs | — | Target ≥40 ✅ |
| Ch.7 Annexes | 🔄 Building | — | Templates + scripts |

---

## GTD Inbox Status

```dataview
LIST
FROM "10 - Inbox"
WHERE file.name != "README-Inbox" AND file.name != "Quick-Capture-Log" AND file.name != "Template-Fleeting-Note"
SORT file.ctime DESC
LIMIT 10
```

---

## Orphan Notes (disconnected — needs linking)

```dataview
LIST
FROM ""
WHERE length(file.inlinks) = 0 AND length(file.outlinks) = 0
SORT file.ctime ASC
LIMIT 10
```

---

## Permanent Notes Created This Month

```dataview
TABLE file.ctime AS "Created"
FROM "30 - Permanent"
WHERE type = "permanent"
AND file.ctime >= date(today) - dur(30 days)
SORT file.ctime DESC
```
