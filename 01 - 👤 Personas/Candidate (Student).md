---
tags:
  - persona
  - candidate
  - student
---

# 👤 Persona: Candidate (Student / Test Taker)

## Profile
Students, job applicants, and certification candidates taking practice quizzes, midterms, or high-stakes assessments.

## Key Objectives & Goals
- Access assessments seamlessly via web links or mobile app deep links.
- Experience a distraction-free, reliable test environment with active timer preservation and autosave.
- Receive immediate scoring and detailed rationales upon submission.

## Primary User Journeys
1. **Joining an Assessment**: [[Flow - Exam Delivery & Live Assessment Player]]
2. **Reviewing Immediate Score & Rationales**: [[Flow - Results Analytics & Feedback Reporting]]

## Key Touchpoints
- Web: [[assessment_frontend (Next.js)]] (`/attempt/[sessionId]`, `/results/[sessionId]`)
- Mobile: [[mobile_app (Expo React Native)]] (`app/exam/[examId].tsx`, `app/attempt/[sessionId].tsx`, `app/results/[sessionId].tsx`)
- Backend Services: [[assessment_backend (FastAPI)]], [[assessment_grading_worker]]
