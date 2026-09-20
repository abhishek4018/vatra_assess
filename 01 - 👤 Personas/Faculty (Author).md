---
tags:
  - persona
  - faculty
  - author
---

# 👤 Persona: Faculty (Author / Educator)

## Profile
Educators, instructional designers, university professors, and corporate trainers who design curriculum assessments.

## Key Objectives & Goals
- Rapidly generate high-quality assessments from lecture slides, textbooks, or custom syllabi.
- Author precise manual questions across standard formats (MCQs, Fill-in-the-Blank, Numeric).
- Review, calibrate difficulty, and tag questions to hierarchical subject taxonomies.
- Publish exam links to students and monitor cohort performance analytics.

## Primary User Journeys
1. **AI Authoring**: [[Flow - AI Assessment Generation (RAG & Gemini)]]
2. **Manual Question Authoring**: [[Flow - Manual Assessment Authoring & Refinement]]
3. **Syllabus / Slide Upload**: [[Flow - Secure Document Upload & Ingestion]]
4. **Cohort Performance Review**: [[Flow - Results Analytics & Feedback Reporting]]

## Key Touchpoints
- UI: [[assessment_frontend (Next.js)]] (`/public`, `/authoring`, `/review`)
- Backend Services: [[assessment_backend (FastAPI)]], [[ai_engine (Gemini + ChromaDB)]]
