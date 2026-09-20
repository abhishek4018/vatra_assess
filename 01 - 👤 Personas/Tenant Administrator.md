---
tags:
  - persona
  - admin
  - tenant
---

# 👤 Persona: Tenant Administrator (Institutional Operator)

## Profile
University department heads, corporate L&D administrators, or platform owners managing tenant organizations and compliance.

## Key Objectives & Goals
- Manage organizational boundaries and institution hierarchies.
- Structure global and tenant-specific subject taxonomies with PostgreSQL `ltree`.
- Monitor AI token quotas, credit wallets, and audit activity.

## Primary User Journeys
1. **Taxonomy & Hierarchy Management**: [[Flow - Multi-Tenant Taxonomy & Hierarchy]]
2. **Billing & Credit Management**: [[Flow - Monetization & Referral Wallet]]

## Key Touchpoints
- UI: [[control_plane (Management & Auth)]] (`/admin`, `/taxonomies`, `/institutions`)
- Backend Services: `control_plane_backend`, `monetization_backend`
