---
tags:
  - entity
  - psychometrics
  - analytics
  - edtech
---

# 📋 Psychometric Item Analysis ($p$-value & $r$-PBIS)

## Overview
Pariksha incorporates automated psychometric analytics calculated after student exam cohorts submit their attempts, validating question quality and detecting defective distractors.

---

## 1. Item Difficulty ($p$-value)
$$p = \frac{R}{N}$$
Where:
- $R$ = Total correct candidate responses.
- $N$ = Total attempts for this question.

### Interpretation Matrix:
| $p$-value Range | Classification | Faculty Recommendation |
| :--- | :--- | :--- |
| $> 0.85$ | Too Easy | Consider increasing distractor plausibility |
| $0.30 - 0.80$ | **Optimal Calibration** | Maintain in active question bank |
| $< 0.30$ | Highly Difficult | Review wording clarity or prerequisite teaching |

---

## 2. Point-Biserial Discrimination ($r$-PBIS)
$$r_{\text{pbis}} = \frac{\bar{X}_1 - \bar{X}_0}{s_X} \sqrt{\frac{N_1 N_0}{N^2}}$$
Where:
- $\bar{X}_1$ = Mean total exam score of candidates who answered this item correctly.
- $\bar{X}_0$ = Mean total exam score of candidates who answered incorrectly.
- $s_X$ = Standard deviation of total exam scores across all candidates.
- $N_1, N_0$ = Counts of candidates answering correctly and incorrectly.

### Interpretation Matrix:
| $r$-PBIS Range | Discrimination Power | Action |
| :--- | :--- | :--- |
| $\ge 0.30$ | **Strong Positive** | Retain item |
| $0.20 - 0.29$ | Moderate | Minor review |
| $0.00 - 0.19$ | Weak | Flag for review |
| $< 0.00$ | **Negative Discrimination** | **Critical Flag**: High performers failed; possible key error or misleading stem |

---

## Related Notes
- Evaluated In: [[Flow - Async Scoring & Psychometric Evaluation]]
- Displayed In: [[Flow - Results Analytics & Feedback Reporting]]
