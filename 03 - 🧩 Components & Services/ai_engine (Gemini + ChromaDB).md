---
tags:
  - component
  - ai
  - llm
  - gemini
  - chromadb
framework: LangChain / Google Gemini / ChromaDB
---

# 🧩 Service: `ai_engine` (Gemini & ChromaDB)

## Overview
Asynchronous AI generation engine responsible for RAG vector retrieval, LLM question generation, JSON schema validation, and automatic self-correction.

## Key Submodules
- `services/rag_service.py` — ChromaDB vector collection querying with dual-tier tenant partitioning (metadata filter & collection sharding).
- `services/generation_service.py` — Prompt assembly, 10-underscore blank enforcement, and multi-model dispatch.
- `services/correction_service.py` — Error feedback loop when LLM responses violate [[Standardized Question Types (EdTech)]] schemas (up to 2 retries).
- `resilience/quota_manager.py` — [[3-Tier LLM Quota Engine]] failover logic (Primary Gemini Pro $\rightarrow$ Secondary Gemini $\rightarrow$ Local Ollama $\rightarrow$ Mock).

## Multi-Tenancy & Vector Isolation
- **Tenant Scope Enforcement**: Embeddings are indexed with `tenant_id` and filtered at query time to prevent cross-tenant context leaks.
- **Similarity Cutoff**: Rejects chunks with cosine similarity $< 0.35$.

## Related Flows
- [[Flow - AI Assessment Generation (RAG & Gemini)]]
- [[Flow - Secure Document Upload & Ingestion]]

