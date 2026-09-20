---
tags:
  - pattern
  - architecture
  - outbox
  - distributed-systems
---

# 📋 Transactional Outbox Pattern

## Problem Statement
In microservices, writing to a database and publishing an event to a message broker (RabbitMQ) within the same user request risks dual-write inconsistencies if the broker is momentarily unavailable or network partitions occur.

## Solution Architecture
Vatra Assess implements the **Transactional Outbox Pattern**:


```mermaid
sequenceDiagram
    autonumber
    participant App as [[assessment_backend (FastAPI)]]
    participant DB as PostgreSQL DB
    participant Relay as assessment_outbox_relay
    participant Broker as RabbitMQ Broker
    participant Worker as [[assessment_grading_worker]]

    App->>DB: BEGIN TRANSACTION
    App->>DB: INSERT into `assessment_sessions` (Submission)
    App->>DB: INSERT into `outbox` (Event: SUBMISSION_COMPLETED, Status: PENDING)
    App->>DB: COMMIT TRANSACTION
    App-->>Client: 200 OK (Accepted)

    loop Polling Loop
        Relay->>DB: SELECT * FROM `outbox` WHERE status = 'PENDING' FOR UPDATE SKIP LOCKED
        Relay->>Broker: Publish message to exchange
        Broker-->>Relay: ACK
        Relay->>DB: UPDATE `outbox` SET status = 'PUBLISHED'
    end

    Broker->>Worker: Dispatch event to grading worker
```

## Guarantees
- **At-Least-Once Delivery**: No events are lost during server crashes or broker outages.
- **Strict Atomicity**: Submission records and outbox events commit together or roll back together.

## Related Flows
- [[Flow - Exam Delivery & Live Assessment Player]]
- [[Flow - Async Scoring & Psychometric Evaluation]]
