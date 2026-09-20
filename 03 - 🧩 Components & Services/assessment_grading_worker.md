---
tags:
  - component
  - worker
  - async
  - amqp
  - grading
broker: RabbitMQ
---

# 🧩 Service: `assessment_grading_worker`

## Overview
Asynchronous background worker consuming exam submission events from RabbitMQ to execute scoring logic, exact/fuzzy text matching, numeric tolerance checks, and real-time psychometric parameter recomputations.

## Responsibilities
- Pulls `SUBMISSION_COMPLETED` messages published via [[Transactional Outbox Pattern]].
- Evaluates candidate answers against master keys for all 5 question types.
- Computes cohort psychometrics: [[Psychometric Item Analysis (p-value & r-PBIS)]].
- Saves immutable evaluation records into `assessment_postgres`.

## Related Flows
- [[Flow - Async Scoring & Psychometric Evaluation]]
- [[Flow - Results Analytics & Feedback Reporting]]
