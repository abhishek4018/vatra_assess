---
tags:
  - flow
  - monetization
  - wallet
  - referrals
flow_id: FLOW-08
domain: Monetization
primary_persona: "[[Tenant Administrator]]"
services_involved:
  - "monetization_backend"
  - "[[assessment_backend (FastAPI)]]"
status: active
---

# 💳 Flow: Monetization & Referral Wallet

## 1. Executive Summary
Manages AI credit consumption, institutional credit packages, educator referral rewards, and ledger accounting across assessment generation and scoring.

---

## 2. Sequence Diagram

```mermaid
sequenceDiagram
    autonumber
    actor User as Educator / Tenant Admin
    participant Frontend as Web App
    participant Monetization as Monetization Backend (:8002)
    participant DB as Postgres Ledger

    User->>Frontend: Trigger AI Assessment Generation / Buy Pack
    Frontend->>Monetization: POST /api/v1/credits/deduct
    Monetization->>DB: Atomic Transaction: Check balance >= cost
    alt Sufficient Credits
        Monetization->>DB: Record debit in ledger & update wallet
        Monetization-->>Frontend: 200 OK (Remaining credits)
        Frontend->>Frontend: Proceed with AI Generation
    else Insufficient Balance
        Monetization-->>Frontend: 402 Payment Required (Prompt Upgrade)
        Frontend-->>User: Show Top-Up Modal / Referral Incentive
    end
```

---

## 3. Key Ledger Rules
- **Double-Entry Accounting**: Every credit granted or consumed has corresponding debit and credit ledger rows.
- **Referral Invariant**: Users who refer educators receive credit grants immediately upon the referred educator's first published assessment.

---

## 4. Related Links
- Component: [[assessment_backend (FastAPI)]]
- Persona: [[Tenant Administrator]], [[Faculty (Author)]]
