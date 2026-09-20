---
tags:
  - component
  - backend
  - fastapi
  - microservice
port: 8000
language: Python / FastAPI
db: PostgreSQL (pgvector)
---

# 🧩 Service: `assessment_backend` (FastAPI)

## Overview
The primary core microservice handling assessment authoring, student attempt session provisioning, and REST API endpoints.

## Core Responsibilities
- CRUD for assessments, questions, and attempt sessions.
- Interaction with `assessment_postgres` (`pgvector` for similarity calculations).
- Enforcing [[Transactional Outbox Pattern]] for event publishing.
- Serving public endpoints for anonymous and authenticated test-takers.

## Key Submodules & API Routers (`app/api/`)
- `public.py` — High-traffic anonymous & viral authoring (`TemporaryCreator`, `quick-generate`, `AssessmentSession`).
- `exams.py` — Enterprise exam blueprints, scheduled assessments, and authenticated `ExamAttempt` lifecycles.
- `questions.py` — Question authoring, review requests (`ReviewRequest`), and versioning (`QuestionVersion`).
- `documents.py` — Document uploads, text extraction, and RAG chunk coordination.
- `payments.py` & `monetization.py` — Public payments, analytics grants, and referral rewards.
- `results.py` — Candidate scorecards, psychometric item metrics, and faculty cohort exports.
- `auth.py` — JWT authentication and role validation.

## Database Entities (`app/models/entities.py`)
- `Question`, `QuestionStats`, `QuestionVersion`, `QuestionTag`
- `Exam`, `AssessmentBlueprint`, `ExamAttempt`, `AssessmentSession`
- `Document`, `ExtractionJob`, `TemporaryCreator`
- `Outbox`, `Score`, `UserWallet`, `ReferralReward`, `PublicPayment`


## Related Flows
- [[Flow - AI Assessment Generation (RAG & Gemini)]]
- [[Flow - Manual Assessment Authoring & Refinement]]
- [[Flow - Exam Delivery & Live Assessment Player]]
