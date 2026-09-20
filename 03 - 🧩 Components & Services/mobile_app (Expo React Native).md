---
tags:
  - component
  - mobile
  - react-native
  - expo
stack: Expo Router / React Native / TypeScript / Zustand / AsyncStorage
---

# 🧩 Service: `mobile_app` (Expo React Native)

## Overview
Cross-platform iOS and Android application optimized for student exam attempts, deep linking (`pariksha://exam/[examId]`), offline-tolerant timer tracking, and instant score breakdown.

## Key Screens & Architecture
- `app/index.tsx` — Exam ID / URL input & quick join lobby.
- `app/exam/[examId].tsx` — Candidate information pre-flight lobby.
- `app/attempt/[sessionId].tsx` — Native exam player with `<AssessmentPlayer>` wrapper, `AppState` background listeners, and native question components.
- `app/results/[sessionId].tsx` — Scorecard, accuracy metrics, Lucide icons, and editable email dispatch.
- `src/store/sessionStore.ts` — Global Zustand state for session questions, timer offsets, and answers map.

## Related Flows
- [[Flow - Exam Delivery & Live Assessment Player]]
- [[Flow - Results Analytics & Feedback Reporting]]
