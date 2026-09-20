---
tags:
  - component
  - frontend
  - nextjs
  - react
port: 3000
framework: Next.js (App Router) / Tailwind CSS / Radix UI
---

# 🧩 Service: `assessment_frontend` (Next.js)

## Overview
The primary web application serving faculty authors, test reviewers, and web-based exam takers.

## Key Modules & Routes
- `/public` — Public landing page & walkthrough tour (`useWalkthroughTour.ts`, `SpotlightOverlay.tsx`).
- `/authoring` & `/review` — Question creation canvas and multi-type question cards (`ManualAuthoringQuestionCard.tsx`).
- `/attempt/[sessionId]` — Web exam player with active timer preservation and autosave.
- `/results/[sessionId]` — Student scorecards, metric gauges, and question breakdowns.

## Related Flows
- [[Flow - AI Assessment Generation (RAG & Gemini)]]
- [[Flow - Manual Assessment Authoring & Refinement]]
- [[Flow - Exam Delivery & Live Assessment Player]]
- [[Flow - Results Analytics & Feedback Reporting]]
