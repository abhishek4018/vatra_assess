---
tags:
  - entity
  - psychometrics
  - irt
  - cat
  - adaptive-testing
  - edtech
---

# 📋 Item Response Theory (IRT) & Computerized Adaptive Testing (CAT)

## 1. Executive Summary
While **Classical Test Theory (CTT)** evaluates fixed-form cohort performance via $p$-value and $r$-PBIS, **Item Response Theory (IRT)** models the probabilistic relationship between a candidate's latent ability ($\theta$) and their likelihood of answering a specific item correctly.

This architecture enables **Computerized Adaptive Testing (CAT)**, where each subsequent question dynamically matches the candidate's estimated proficiency level.

---

## 2. 3-Parameter Logistic (3PL) IRT Model

The probability $P_i(\theta)$ that a candidate with ability $\theta$ answers item $i$ correctly is modeled as:

$$P_i(\theta) = c_i + \frac{1 - c_i}{1 + e^{-D \cdot a_i (\theta - b_i)}}$$

Where:
- $\theta \in (-\infty, +\infty)$: Latent candidate ability (standardized scale, mean $= 0$, std dev $= 1$).
- $b_i \in [-3.0, +3.0]$: **Item Difficulty Parameter** (the ability level where candidate has a 50% chance of answering correctly above guessing).
- $a_i \in (0.0, 2.5]$: **Item Discrimination Parameter** (slope of the Item Characteristic Curve at $b_i$).
- $c_i \in [0.0, 0.35]$: **Pseudo-Guessing Parameter** (lower asymptote for multiple-choice formats).
- $D = 1.7$: Scaling factor aligning logistic metric to the normal ogive.

---

## 3. CAT Adaptive Testing Loop

```mermaid
flowchart TD
    Start["Candidate Begins Exam (Initial Ability θ₀ = 0.0)"] --> Select["Select Next Item with Maximum Fisher Information I(θ)"]
    Select --> Present["Present Item to Candidate"]
    Present --> Response["Candidate Submits Response (Correct / Incorrect)"]
    Response --> Recompute["Update Ability Estimate θ̂ via Bayes EAP / Newton-Raphson MLE"]
    Recompute --> Check{"Stopping Rule Met?"}
    
    Check -->|No (Standard Error SE(θ̂) > Benchmark OR Min Items Not Met)| Select
    Check -->|Yes (SE(θ̂) ≤ 0.20 OR Max Items Reached)| Conclude["Conclude Exam & Generate Scaled Proficiency Score"]
```

---

## 4. Item Information Function (IIF)

The Fisher Information $I_i(\theta)$ measures how much precision item $i$ provides at ability level $\theta$:

$$I_i(\theta) = \frac{D^2 a_i^2 (1 - c_i) P_i(\theta) Q_i(\theta)}{\left(c_i + (1 - c_i) P_i(\theta)\right)^2}$$

Where $Q_i(\theta) = 1 - P_i(\theta)$. The adaptive engine selects the item from the active pool that maximizes $\sum I_i(\hat{\theta})$ subject to taxonomy constraints.

---

## 5. Comparison: CTT vs IRT

| Dimension | Classical Test Theory (CTT) | Item Response Theory (IRT) |
| :--- | :--- | :--- |
| **Primary Metrics** | $p$-value (difficulty), $r$-PBIS (discrimination) | $b_i$ (difficulty), $a_i$ (discrimination), $c_i$ (guessing) |
| **Sample Dependency** | Group-dependent (varies with student cohort) | **Sample-independent** (item parameters are invariant) |
| **Test Format** | Fixed-form exams (all students get same items) | **Adaptive testing** (customized item sequence per student) |
| **Precision** | Single Standard Error of Measurement ($SEM$) | Precision $SE(\theta)$ is a function of ability $\theta$ |
| **Vatra Implementation** | Live Async Grading Worker | Adaptive Engine Extension Roadmap |

---

## 6. Related Notes
- Foundation: [[Psychometric Item Analysis (p-value & r-PBIS)]]
- Delivery Engine: [[Flow - Exam Delivery & Live Assessment Player]]
- Question Bank: [[Standardized Question Types (EdTech)]]
