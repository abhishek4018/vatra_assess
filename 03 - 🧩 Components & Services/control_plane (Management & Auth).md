---
tags:
  - component
  - admin
  - multi-tenant
  - control-plane
port: 8001 (backend) / 3001 (frontend)
---

# 🧩 Service: `control_plane` (Management & Auth)

## Overview
The institutional management microservice managing tenants, users, license keys, and hierarchical subject taxonomies using PostgreSQL `ltree`.

## Key Capabilities
- Tenant provisioning and domain mapping.
- Organization and departmental hierarchical structures.
- Subject taxonomy trees with GIST index acceleration.

## Related Flows
- [[Flow - Multi-Tenant Taxonomy & Hierarchy]]
- [[Flow - Monetization & Referral Wallet]]
