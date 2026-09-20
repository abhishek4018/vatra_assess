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
- `services/rag_service.py` — ChromaDB vector collection querying with tenant partitioning.
- `services/generation_service.py` — Prompt assembly and multi-model dispatch.
- `services/correction_service.py` — Error feedback loop when LLM responses violate [[Standardized Question Types (EdTech)]] schemas.
- `resilience/quota_manager.py` — [[3-Tier LLM Quota Engine]] failover logic.

## Related Flows
- [[Flow - AI Assessment Generation (RAG & Gemini)]]
- [[Flow - Secure Document Upload & Ingestion]]
