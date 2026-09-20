---
tags:
  - pattern
  - resilience
  - ai
  - quota
---

# 📋 3-Tier LLM Quota Resilience Engine

## Overview
To prevent generation outages caused by upstream Gemini API rate limits (HTTP 429) or token quota exhaustion, Vatra Assess implements a 4-level cascading fallback engine.


```mermaid
flowchart TD
    Req["Generate Question Prompt"] --> T1{"Tier 1: Primary Gemini API"}
    T1 -->|Success (200 OK)| Return["Return Questions"]
    T1 -->|HTTP 429 / Quota Error| T2{"Tier 2: Secondary Gemini Key"}
    
    T2 -->|Success (200 OK)| Return
    T2 -->|Quota Exhausted| T3{"Tier 3: Local Ollama (llama3.2:3b)"}
    
    T3 -->|Success| Return
    T3 -->|Ollama Offline| T4["Tier 4: MOCK_LLM_WORKER"]
    T4 --> Return
```

---

## Tier Definitions
1. **Tier 1 (Primary Gemini Pro Key)**: Highest quality, low latency, default model.
2. **Tier 2 (Secondary Gemini Key)**: Instant fallback if primary key hits rate limits or billing thresholds.
3. **Tier 3 (Local Ollama Engine)**: Self-hosted local container fallback (`llama3.2:3b`) ensuring zero cloud reliance during network disruptions.
4. **Tier 4 (Mock Generator)**: Seeded deterministic mock response generator for offline development and CI/CD pipelines.

---

## Related Notes
- Used In: [[Flow - AI Assessment Generation (RAG & Gemini)]]
- Component: [[ai_engine (Gemini + ChromaDB)]]
