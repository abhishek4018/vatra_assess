---
tags:
  - flow
  - rag
  - ingestion
  - documents
flow_id: FLOW-03
domain: Ingestion
primary_persona: "[[Faculty (Author)]]"
services_involved:
  - "[[assessment_frontend (Next.js)]]"
  - "[[assessment_backend (FastAPI)]]"
  - "[[ai_engine (Gemini + ChromaDB)]]"
status: active
---

# 📄 Flow: Secure Document Upload & Ingestion

## 1. Executive Summary
Handles the parsing, sanitization, recursive chunking, and vector embedding of PDFs, PPTXs, and DOCX curriculum documents into tenant-isolated ChromaDB collections.

---

## 2. Sequence Diagram

```mermaid
sequenceDiagram
    autonumber
    actor Faculty as [[Faculty (Author)]]
    participant UI as [[assessment_frontend (Next.js)]]
    participant Backend as [[assessment_backend (FastAPI)]]
    participant Storage as File / S3 Storage
    participant Chroma as ChromaDB Vector Store

    Faculty->>UI: Drag & Drop Syllabus/Slides (PDF, DOCX, TXT)
    UI->>Backend: POST /api/v1/documents/upload (multipart/form-data)
    Backend->>Storage: Store source artifact
    Backend->>Backend: Extract raw text & sanitize
    Backend->>Backend: Chunk with LangChain RecursiveCharacterTextSplitter (chunk_size=1000, overlap=150)
    Backend->>Backend: Compute embeddings (text-embedding-004)
    Backend->>Chroma: Insert vectors with metadata: {tenant_id, creator_id, doc_id}
    Backend-->>UI: Return Document Ready (chunks_indexed, doc_id)
    UI-->>Faculty: Display "Ready to Generate Assessment" badge
```

---

## 3. Key Technical Invariants & Vector Sharding Architecture

> [!IMPORTANT] **CTO Invariant: Multi-Tenant Vector Isolation & Sharding Roadmap**
> To ensure strict FERPA/GDPR institutional compliance and prevent cross-institution context hallucination, vector retrieval enforces a dual-tier partitioning model:

1. **Tier 1: Metadata-Filtered Shared Index (Current Base Scale)**:
   - Vectors in ChromaDB are tagged with metadata: `{"tenant_id": "...", "creator_id": "...", "doc_id": "..."}`.
   - All ANN (Approximate Nearest Neighbor) cosine similarity searches enforce a mandatory `$eq` filter on `tenant_id`.
   - Cosine threshold: Chunks with similarity score $< 0.35$ are discarded to prevent irrelevant distractors.
2. **Tier 2: Dedicated Collection Sharding (Enterprise Scale $> 10k$ Tenants)**:
   - For high-volume enterprise university tenants, the vector store dynamically provisions an isolated collection `tenant_{tenant_id}_docs`.
   - Eliminates index scanning contention across tenants and supports tenant-specific embedding model fine-tuning.
3. **Data Lifecycle & Vector Purge Policy**:
   - Deleting a `Document` entity triggers an atomic vector purge in ChromaDB (`where={"doc_id": doc_id}`) alongside S3 raw document deletion.


---

## 4. API Endpoints & Models
- `POST /api/v1/public/documents/extract` (`UploadFile` $\rightarrow$ `ExtractionJobResponse`) — Multi-part document upload creating an async `ExtractionJob`.
- `GET /api/v1/public/documents/jobs/{job_id}` — Polling job status until extraction and chunk embedding complete.
- `POST /api/v1/documents/upload` — Authenticated faculty document repository ingestion.
- Database Entity: `Document` and `ExtractionJob` in `assessment_postgres`.

## 5. Related Links
- Next Step: [[Flow - AI Assessment Generation (RAG & Gemini)]]
- Component: [[ai_engine (Gemini + ChromaDB)]]

