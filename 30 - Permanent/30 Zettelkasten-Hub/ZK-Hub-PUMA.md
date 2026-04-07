---
id: ZK-Hub-PUMA
title: "🗃️ Zettelkasten Hub — PUMA Research Knowledge Base"
type: zettelkasten-hub
tags: [zettelkasten, hub, moc, knowledge-base, puma]
created: 2026-04-06
updated: 2026-04-06
---

# 🗃️ Zettelkasten Hub — PUMA Research Knowledge Base

> **Zettelkasten principle** (Niklas Luhmann, 1927–1998): knowledge grows through atomic, permanently linked notes. Each note = one idea. Notes never move. Links create emergent insight.
>
> **This hub** follows the [Obsidian Zettelkasten Starter Kit](https://github.com/groepl/Obsidian-Zettelkasten-Starter-Kit) pattern by Edmund Gröpl, adapted for the PUMA Project research context.

---

## 🗂️ Zettelkasten Note Types (adapted from groepl)

| Type | Prefix | Location | Purpose |
|------|--------|----------|---------|
| **Fleeting Note** | `FL-` | `10 - Inbox/Fleeting-Notes/` | Raw capture, process within 48h |
| **Literature Note** | `LN-` | `20 - Literature/` | External source processed with Keshav |
| **Permanent Note** | `PN-` | `30 - Permanent/31–33/` | Your synthesised atomic idea |
| **Structure Note** | `ST-` | `30 - Permanent/30 Zettelkasten-Hub/` | Index / hub for a cluster of PN |
| **Source Note** | `SRC-` | `30 - Permanent/36 Sources/` | Full source metadata (author, year, context) |
| **Person Note** | `PER-` | `30 - Permanent/37 Persons/` | Key thinkers (Keshav, Flyvbjerg, Luhmann…) |
| **MOC** | `MOC-` | `80 - MOC/` | Navigation map across note clusters |

---

## 📋 PUMA Permanent Notes Index

### 31 Concepts — Core Ideas

```dataview
TABLE file.ctime AS "Created", tags AS "Tags"
FROM "30 - Permanent/31 Concepts"
WHERE type = "permanent"
SORT file.ctime DESC
```

### 32 Methods — Research & Statistical

```dataview
TABLE file.ctime AS "Created"
FROM "30 - Permanent/32 Methods"
WHERE type = "permanent"
SORT file.name ASC
```

### 33 Frameworks — Methodologies & Prompting

```dataview
TABLE file.ctime AS "Created"
FROM "30 - Permanent/33 Frameworks"
WHERE type = "permanent"
SORT file.name ASC
```

---

## 🔗 Zettelkasten Rules (PUMA adaptation)

1. **One idea per note**. If a note wants to say two things, split it.
2. **Declarative title**. The title IS the claim. Example: ✅ "RAG retrieval improves precision when examples are structurally similar to the query" ❌ "RAG notes"
3. **Never move a permanent note**. It lives in `30 - Permanent/` forever. Projects archive; knowledge does not.
4. **Always link**. Every permanent note must link to: its source LN, at least one related PN, and one MOC.
5. **Write in your own words**. No copy-paste from sources. If you can't restate it, you don't understand it yet.
6. **Distinguish claim from evidence**. State the idea, then support it. Never bury the claim in the middle.

---

## 🌐 Knowledge Graph Status

```dataview
TABLE length(file.inlinks) AS "Inlinks", length(file.outlinks) AS "Outlinks"
FROM "30 - Permanent"
WHERE type = "permanent"
SORT length(file.inlinks) DESC
LIMIT 15
```

---

## 🔍 Orphan Notes (no links — needs integration)

```dataview
LIST
FROM "30 - Permanent"
WHERE length(file.inlinks) = 0 AND length(file.outlinks) = 0
SORT file.ctime ASC
```

---

## 📚 Source Notes Index

```dataview
TABLE author AS "Author", year AS "Year", type AS "Type"
FROM "30 - Permanent/36 Sources"
SORT year DESC
```

---

## 👤 Person Notes Index

```dataview
TABLE role AS "Role", field AS "Field"
FROM "30 - Permanent/37 Persons"
SORT file.name ASC
```

---

## 🗺️ Related MOCs

- [[80 - MOC/81 Topic-Maps/MOC-PUMA-Master]]
- [[80 - MOC/81 Topic-Maps/MOC-Methods-Frameworks]]
- [[80 - MOC/81 Topic-Maps/MOC-Literature-Review]]
- [[80 - MOC/81 Topic-Maps/MOC-Zettelkasten-PUMA]]
