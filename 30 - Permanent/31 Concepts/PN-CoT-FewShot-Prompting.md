---
id: PN-Chain-of-Thought
title: "Chain-of-Thought (CoT) Prompting"
type: permanent-note
category: concept
tags: [permanent, concept, prompting, cot, reasoning, llm]
aliases: ["CoT", "Chain of Thought", "Zero-Shot CoT", "Step-by-step reasoning"]
created: 2026-03-01
maturity: evergreen
sources: ["[[LN-Wei2022-CoT]]", "[[LN-Brown2020-GPT3-FewShot]]"]
---

# Chain-of-Thought (CoT) Prompting

> **Atomic claim:** Instructing a language model to reason step-by-step before producing a final answer (CoT) consistently improves performance on tasks requiring multi-step inference — including issue triage and effort estimation — compared to direct answer prompting.

---

## 💡 The Concept

Chain-of-Thought prompting elicits intermediate reasoning steps from LLMs before they produce a final answer. Two main variants:

### Zero-Shot CoT
Add a simple trigger to the prompt — no examples needed:
```
"Think step by step before giving your final answer."
"Let's reason through this carefully:"
"Walk me through your reasoning before classifying:"
```

### Few-Shot CoT
Provide examples where the reasoning chain is shown:
```
Example 1:
Issue: "Login page returns 500 error for all users"
Reasoning: This affects all users (scope: entire system), 
           is a hard blocker (severity: critical), 
           is a production system (environment: prod).
Priority: Critical

Example 2:
Issue: "Dashboard graph legend overlaps text on mobile"
Reasoning: This is a visual issue (severity: minor),
           affects only mobile users (scope: partial),
           has a workaround (pinch to zoom).
Priority: Low

Now classify:
Issue: [NEW ISSUE]
Reasoning: [MODEL GENERATES HERE]
Priority: [FINAL ANSWER]
```

---

## 📊 Relevance to PUMA

| Strategy | H1 Test | Expected Effect |
|----------|---------|----------------|
| Zero-shot (no CoT) | Baseline comparison | Lower F1 |
| Zero-shot CoT | Experimental condition | Moderate improvement |
| Few-shot-3 | Experimental condition | Significant improvement |
| Few-shot-6 CoT | Experimental condition | Highest F1 expected |

**Key research question:** Does CoT help more with triage (classification) or estimation (regression proxy)?

**Key reference:** Wei et al. (2022) show CoT gains are most pronounced for models ≥100B parameters — may be limited for 7-8B local models like Llama 3.2 and Mistral 7B. This is a testable prediction in PUMA H1.

---

## 🔗 Connected Ideas

**Extends:** [[PN-Few-Shot-Prompting]] | **Used in:** [[60 - Resources/61 Prompts/PT-PUMA-Triage-CoT]]
**Tested in:** [[40 - Projects/PUMA/41.7 Experiments/EX-Stage1-Triage-Overview]]
**Contrasts with:** Zero-shot direct prompting | **Enabled by:** [[PN-RCOIF-Framework]] (I component)

---
---
id: PN-Few-Shot-Prompting
title: "Few-Shot Prompting"
type: permanent-note
category: concept
tags: [permanent, concept, prompting, few-shot, in-context-learning, llm]
aliases: ["Few-Shot", "In-Context Learning", "ICL", "k-shot"]
created: 2026-03-01
maturity: evergreen
---

# Few-Shot Prompting

> **Atomic claim:** Providing k labelled examples (k=3,6) within the prompt context enables LLMs to adapt their classification behaviour to the target task distribution without gradient updates — a form of in-context learning that is the primary variable being manipulated in PUMA Stages 1 and 2.

---

## 💡 The Concept

Few-shot prompting places k (input, label) pairs in the prompt before the test instance. The model uses these as implicit demonstrations of the desired mapping.

**Why it works:** LLMs learn to identify the pattern (task format, label space, reasoning style) from demonstrations and apply it to novel instances.

**Key design decisions for PUMA:**
1. **Example selection** — Stratified sampling (one per priority class for k=4, two per class for k=8)
2. **Example ordering** — Random order to prevent recency bias
3. **Example diversity** — Cover edge cases, not just easy examples
4. **Label format** — Consistent with expected output format

---

## 📋 Template for Issue Triage (k=3)

```
You are an expert software project manager. 
Classify the priority of Jira issues.

Priority classes: Critical | High | Medium | Low

Examples:
---
Issue: "Database connection pool exhausted — 100% of API requests failing"
Priority: Critical

Issue: "Search results take 8 seconds to load instead of 2 seconds"
Priority: High  

Issue: "Tooltip text is cut off at the right edge in Firefox"
Priority: Low
---

Now classify this issue:
Issue: "{issue_title} — {issue_description}"
Priority:
```

---

## 🔗 Connected Ideas

**Complements:** [[PN-Chain-of-Thought]] | **Contrasts with:** Zero-shot
**Reference:** [[LN-Brown2020-GPT3-FewShot]] | **Tested in:** [[60 - Resources/61 Prompts/PT-PUMA-Triage-FewShot3]]
**Key paper:** Calikli & Alhamed (2025) — request format affects estimation non-monotonically → [[LN-Calikli2025-RequestFormats]]
