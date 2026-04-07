---
id: EX-Hypotheses-H1-H2
title: "PUMA Research Hypotheses — H1 (Triage) & H2 (Estimation)"
type: experiment
tags: [experiment, hypothesis, h1, h2, falsifiability, wilcoxon]
stage: "both"
status: planned
created: 2026-03-01
updated: 2026-03-01
---

# PUMA Research Hypotheses — H1 & H2

> **Main research question:** Are there statistically significant differences in quality of automatic issue triage and effort estimation when using different LLMs and prompting strategies, evaluated on real ICT project datasets with verified reference labels?

---

## H1 — Issue Triage Hypothesis

### Formulation (Popper falsifiability framework)

**H₀₁ (Null — refutable):**
No LLM + strategy configuration will achieve F1-macro superior to the keyword-based heuristic baseline on Jira SR. Any observed difference is explained by random variation (Wilcoxon bilateral test, α = 0.05).

**H₁ (Alternative):**
At least one configuration achieves F1-macro statistically superior (p < 0.05) to the heuristic baseline, with effect size r ≥ 0.1 computed over per-class score distributions.

**Falsification condition:**
If NO configuration beats the baseline with statistical significance under the defined protocol, H₀₁ is NOT rejected. Conclusion: local LLMs evaluated do not provide measurable improvement over keyword heuristics under these conditions.

### Operational Variables

| Variable type | Variable | Value/Range |
|--------------|----------|------------|
| **Independent** | LLM model | {llama3.2:8b, mistral:7b} |
| **Independent** | Prompting strategy | {zero-shot, few-shot-3, few-shot-6, cot} |
| **Dependent** | F1-macro | 0.0–1.0 |
| **Dependent** | Precision per class | 0.0–1.0 |
| **Dependent** | Recall per class | 0.0–1.0 |
| **Control** | seed | 42 |
| **Control** | temperature | 0 |
| **Control** | Dataset subset | 200 issues, stratified (50/class) |
| **Control** | Hardware | 16GB RAM CPU |

### Baseline Definition

**Heuristic baseline** (keyword classifier):
```python
PRIORITY_KEYWORDS = {
    'Critical': ['crash', 'down', 'production', 'all users', 'data loss', 
                 'security', 'outage', 'failing', '500 error'],
    'High': ['slow', 'performance', 'timeout', 'broken', 'cannot', 'fails'],
    'Low': ['typo', 'colour', 'color', 'alignment', 'documentation', 'tooltip']
}
# Default: Medium
```

Expected baseline F1-macro: 0.45–0.52 (to be calculated on subset before experiments)

### MVP Threshold

| Threshold | Value | Status |
|-----------|-------|--------|
| Minimum (MVP) | F1-macro ≥ 0.55 | Required for MVP success |
| Desired | F1-macro ≥ 0.70 | Target for quality contribution |

---

## H2 — Effort Estimation Hypothesis

### Formulation

**H₀₂ (Null — refutable):**
No few-shot configuration will achieve MAE below the project historical mean as estimator on TAWOS. Any difference is random variation (Wilcoxon bilateral, α = 0.05).

**H₂ (Alternative):**
At least one few-shot configuration achieves MAE statistically below the historical mean (p < 0.05), with absolute reduction ≥ 0.5 story points as practical relevance threshold.

### Operational Variables

| Variable type | Variable | Value/Range |
|--------------|----------|------------|
| **Independent** | LLM model | {llama3.2:8b, mistral:7b} |
| **Independent** | Prompting strategy | {zero-shot, few-shot-3, cot} |
| **Dependent** | MAE (story points) | ≥ 0.0 SP |
| **Dependent** | RMSE | ≥ 0.0 SP |
| **Control** | seed, temperature | 42, 0 |
| **Control** | Fibonacci scale | {1,2,3,5,8,13,21} |

### Reference Baselines

| Baseline | MAE | Source |
|---------|-----|--------|
| Historical mean per project | ~3.5 SP | TAWOS dataset statistics |
| Deep-SE | ~3.2 SP | Choetkiertikul et al. (2018) |
| CoGEE (GPT-4) | ~1.9 SP | Tawosi et al. (2024) |
| **PUMA minimum (H2)** | ≤ 3.0 SP | MVP threshold |
| **PUMA desired** | ≤ 1.5 SP | Competitive with CoGEE |

---

## Statistical Analysis Protocol

### Test: Wilcoxon Signed-Rank

```python
from scipy import stats
import numpy as np

def test_hypothesis(model_scores: list, baseline_scores: list, 
                    alpha: float = 0.05) -> dict:
    """
    Two-sided Wilcoxon signed-rank test per PUMA protocol.
    Effect size r = Z / sqrt(N) where Z is from normal approximation.
    """
    stat, p_value = stats.wilcoxon(model_scores, baseline_scores, 
                                    alternative='two-sided')
    N = len(model_scores)
    # Approximate Z for effect size
    z = stats.norm.ppf(1 - p_value/2)
    effect_r = abs(z) / np.sqrt(N)
    
    return {
        'statistic': stat,
        'p_value': p_value,
        'effect_size_r': effect_r,
        'is_significant': p_value < alpha,
        'effect_category': 'small' if effect_r < 0.3 else 
                          'medium' if effect_r < 0.5 else 'large',
        'h0_rejected': p_value < alpha and effect_r >= 0.1
    }
```

### Reporting Standards (Kitchenham et al., 2002)

Every result table must report:
- N (sample size)
- Mean ± SD for both conditions
- Wilcoxon W statistic
- p-value (exact, not "> 0.05")
- Effect size r with confidence interval
- Practical significance threshold met? (Y/N)

---

## Experiment Tracking

```dataview
TABLE model, strategy, f1_macro, mae, wilcoxon_p, status
FROM "40 - Projects/PUMA/41.7 Experiments"
WHERE type = "experiment"
SORT stage ASC, f1_macro DESC
```

---

## 🔗 Related Notes

[[40 - Projects/PUMA/41.7 Experiments/EX-Stage1-Triage-Overview]]
[[40 - Projects/PUMA/41.7 Experiments/EX-Stage2-Effort-Overview]]
[[20 - Literature/20.3 Datasets/LN-Datasets-JiraSR-TAWOS]]
[[30 - Permanent/35 Hypotheses/PN-Falsifiability-Popper]]
