---
id: MOC-Research-Pipeline
title: "🔬 MOC — Research Pipeline"
type: moc
tags: [moc, research, ebse, dsr, slr, prisma, pipeline]
created: 2026-03-01
updated: 2026-03-01
---

# 🔬 Research Pipeline Map of Content

> This MOC maps the complete research methodology pipeline used in PUMA, combining three integrated frameworks.

---

## Framework 1 — Evidence-Based Research Augmented by AI (EBSE + PRISMA-trAIce)

```
Phase 0: Problem Definition
    └── FINER criteria validation
    └── Research question formulation
    └── Falsifiable hypotheses (Popper)
          ↓
Phase 1: Systematic Literature Review (SLR)
    └── PRISMA 2020 protocol
    └── PRISMA-DFLLM extension (AI-assisted screening)
    └── PRISMA-trAIce (AI use documentation)
          ↓
Phase 2: Gap Analysis
    └── Reproducibility gap
    └── Prompting strategy gap
    └── Carbon footprint gap
          ↓
Phase 3: Methodological Design (DSR)
    └── Artefact specification (SDD/BDD)
    └── Experiment design
          ↓
Phase 4: Experimentation
    └── Controlled conditions
    └── Statistical analysis (Wilcoxon)
    └── Carbon measurement (CodeCarbon)
          ↓
Phase 5: Evaluation & Discussion
    └── H1, H2 testing
    └── Validity analysis
    └── Replicability verification
```

**Key notes:**
- [[30 - Permanent/32 Methods/PN-SLR-PRISMA]] — SLR protocol
- [[30 - Permanent/32 Methods/PN-FINER-Criteria]] — Research question quality
- [[30 - Permanent/33 Frameworks/PN-PRISMA-DFLLM]] — AI-augmented PRISMA
- [[40 - Projects/PUMA/41.2 Literature-Review/PR-PUMA-Ch2-Literature]] — SLR execution

---

## Framework 2 — Design Science Research + SDD/BDD + AI Agents

```
DSR Cycle (Hevner 2004 + Peffers 2007):
    Problem → Objectives → Design & Development → Demonstration → Evaluation → Communication

SDD Chain:
    Spec-First Design
        └── OpenSpec format
        └── Spec Kit validation
        └── BDD scenarios (Given/When/Then)
        └── TDD test cases
              ↓
    AI-Assisted Generation
        └── Agent generates code/specs from prompts
        └── Human validates (Human-in-the-Loop)
        └── Red Teaming (rival hypotheses)
              ↓
    BMAD Workflow
        └── Brainstorm → Map → Architect → Develop
```

**Key notes:**
- [[30 - Permanent/32 Methods/PN-DSR-Method]] — DSR paradigm
- [[30 - Permanent/33 Frameworks/PN-SDD-Framework]] — Spec-Driven Development
- [[30 - Permanent/33 Frameworks/PN-BDD-Framework]] — Behaviour-Driven Development
- [[30 - Permanent/33 Frameworks/PN-BMAD-Framework]] — BMAD workflow
- [[40 - Projects/PUMA/41.6 Specs/SP-Architecture-v1]] — PUMA architecture

---

## Framework 3 — MIT Student Method as Cognitive Operator

The MIT Student Method operates at three levels in PUMA:

| Level | Application | Tools |
|-------|------------|-------|
| **Reading/Synthesis** | Cornell notes + DRCA on each paper | [[30 - Permanent/33 Frameworks/PN-Cornell-Method]] |
| **AI Interaction** | RCOIF/RCOF + EGI + AMI + IIPR patterns | [[30 - Permanent/33 Frameworks/PN-RCOIF-Framework]] |
| **Red Teaming** | Rival hypotheses, counter-evidence search | [[30 - Permanent/33 Frameworks/PN-Red-Teaming]] |

**Key notes:**
- [[30 - Permanent/33 Frameworks/PN-MIT-Student-Method]] — Full method
- [[30 - Permanent/33 Frameworks/PN-EGI-Framework]] — Guided Interactive Exploration
- [[30 - Permanent/33 Frameworks/PN-AMI-Framework]] — Autodiagnosis & Iterative Improvement
- [[30 - Permanent/33 Frameworks/PN-DRCA-Framework]] — Deconstruction & Reconstruction

---

## Phase-to-Framework Mapping

| PUMA Phase | Primary Framework | MIT Student Method Role |
|------------|------------------|------------------------|
| F0 Initiation | EBSE/SLR | Panoramic mapping + screening |
| F1 Design | DSR + SDD | Cornell on requirements → BDD stories |
| F2 Prototype | DSR + BDD/TDD | CoT + Few-Shot for spec generation |
| F3 Extension | DSR + BMAD | IIPR + AMI for agent iteration |
| F4 Analysis | EBSE + Stats | DRCA on results |
| F5 Closure | Full integration | Red teaming conclusions |

---

## AI Use Documentation (per PRISMA-trAIce)

```dataview
TABLE tool, phase, purpose, validation
FROM "50 - Areas/51 Research"
WHERE type = "ai-use-log"
SORT phase ASC
```
