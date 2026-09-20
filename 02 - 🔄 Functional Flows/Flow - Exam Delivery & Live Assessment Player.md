---
tags:
  - flow
  - delivery
  - exam-player
  - mobile
  - web
flow_id: FLOW-04
domain: Delivery
primary_persona: "[[Candidate (Student)]]"
services_involved:
  - "[[assessment_frontend (Next.js)]]"
  - "[[mobile_app (Expo React Native)]]"
  - "[[assessment_backend (FastAPI)]]"
  - "[[assessment_grading_worker]]"
status: active
---

# ⏱️ Flow: Exam Delivery & Live Assessment Player

## 1. Executive Summary
Covers the candidate experience from accessing the exam link/deep link, entering lobby details, taking the timed assessment across Web and Mobile apps, maintaining client-side timer persistence, and auto-submitting.

---

## 2. Sequence Diagram

```mermaid
sequenceDiagram
    autonumber
    actor Candidate as [[Candidate (Student)]]
    participant Client as [[assessment_frontend (Next.js)]] / [[mobile_app (Expo React Native)]]
    participant Store as Zustand / AsyncStorage Store
    participant Backend as [[assessment_backend (FastAPI)]]
    participant Outbox as [[Transactional Outbox Pattern]]

    Candidate->>Client: Open Exam URL / Deep Link (`pariksha://exam/{id}`)
    Client->>Backend: GET /api/v1/public/assessments/{id}
    Backend-->>Client: Assessment Metadata (Title, Duration, Question Count)
    Client-->>Candidate: Show Exam Lobby Screen (Name, Email, Instructions)
    
    Candidate->>Client: Click "Start Assessment"
    Client->>Backend: POST /api/v1/public/sessions/start
    Backend-->>Client: Session Created (`sessionId`, sanitized questions without answer keys)
    
    Client->>Store: Initialize Local Timer, Sync Timestamp, Answers Map
    Client-->>Candidate: Render Question 1 of N in `<AssessmentPlayer>`
    
    loop During Assessment
        Candidate->>Client: Select / Enter Answer
        Client->>Store: Save local answer state & touch timestamp
        Client->>Backend: PATCH /api/v1/public/sessions/{sessionId} (Auto-sync snapshot)
    end
    
    alt Time Expires OR Candidate Clicks Submit
        Client->>Candidate: Confirm Submission Modal
        Candidate->>Client: Submit Final Answers
        Client->>Backend: POST /api/v1/public/sessions/{sessionId}/submit
        Backend->>Backend: Record Submission in DB
        Backend->>Outbox: Write `SUBMISSION_COMPLETED` event
        Backend-->>Client: Return Immediate Score / Submission Acknowledged
        Client-->>Candidate: Redirect to [[Flow - Results Analytics & Feedback Reporting]]
    end
```

---

## 3. Critical Client-Side Features & Safeguards

1. **Active Timer Resilience**:
   - Web uses `localStorage` timestamp offsets.
   - Mobile uses `AppState` listeners + `AsyncStorage` to ensure timers do not reset if the student switches apps or backgrounds their phone.
2. **5 Question Types Rendered**:
   - `MCQ_SINGLE`: Radio options with active highlight.
   - `MCQ_MULTIPLE`: Multi-select check toggles.
   - `TEXT_ENTRY`: Auto-focused text input.
   - `INLINE_CHOICE`: Inline pickers with WCAG AA 44px minimum touch targets.
   - `NUMERIC_ENTRY`: Number pad with float support (`step="any"`).
3. **Leave Confirmation**:
   - React Native `BackHandler` and Web `beforeunload` intercept unintended exits.

---

## 4. API Endpoints & Dual Delivery Models

### A. Public / Fast-Access Mode (`AssessmentSession`)
- `GET /api/v1/public/exams/{examId}` — Fetch public exam metadata.
- `POST /api/v1/public/sessions/start` (`PublicSessionStartRequest`) — Start candidate session.
- `PATCH /api/v1/public/sessions/{sessionId}` (`PublicSessionUpdateRequest`) — Real-time progress snapshot.
- `POST /api/v1/public/sessions/{sessionId}/submit` — Final submission.

### B. Enterprise / Authenticated Mode (`ExamAttempt`)
- `GET /api/v1/exams/{examId}` (`ExamDetailResponse`) — Institutional exam schema.
- `POST /api/v1/exams/{examId}/attempts/start` (`ExamAttemptStartRequest`) — Start verified student attempt.
- `POST /api/v1/exams/{examId}/attempts/{attemptId}/progress` (`ExamAttemptProgressRequest`) — Auto-save payload.
- `POST /api/v1/exams/{examId}/attempts/{attemptId}/submit` (`ExamAttemptSubmitRequest`) — Submit for grading.

## 5. Related Links
- Next Step: [[Flow - Async Scoring & Psychometric Evaluation]]
- Frontend Components: [[assessment_frontend (Next.js)]], [[mobile_app (Expo React Native)]]

