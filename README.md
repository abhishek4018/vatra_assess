# 🎓 Vatra Assess Functional Flow Knowledge Base (Obsidian Vault)

An interconnected Obsidian knowledge base documenting the functional flows, system personas, microservice interactions, standardized EdTech question models, and automated psychometric evaluation engine for the **Vatra Assess Platform**.


---

## 🗺️ What's Inside

- **00 - 🗺️ Home & Index.md**: Central Map of Content (MOC) and ecosystem map.
- **01 - 👤 Personas/**: Detailed profiles, objectives, and touchpoints for Faculty (Authors), Candidates (Students), and Tenant Administrators.
- **02 - 🔄 Functional Flows/**: Deep-dive sequence diagrams, step-by-step lifecycles, and API contracts:
  - AI Assessment Generation (RAG + Gemini 3-tier fallback)
  - Manual Assessment Authoring & Walkthrough
  - Secure Document Upload & Extraction Jobs
  - Exam Delivery & Live Assessment Player (Web & Mobile)
  - Async Scoring & Psychometric Evaluation
  - Candidate Results & Feedback Reporting
  - Multi-Tenant Taxonomy (PostgreSQL `ltree`)
  - Monetization & Credit Wallet
- **03 - 🧩 Components & Services/**: FastAPI backend, Next.js frontend, AI Engine, Mobile React Native App, AMQP workers, and Control Plane.
- **04 - 📋 Entities & Patterns/**: Standardized 5 Question Types (MCQ, FIB, FIBAN, FIBN), Transactional Outbox pattern, Psychometric Item Analysis ($p$-value & $r$-PBIS), and 3-Tier Quota Engine.
- **05 - 🎨 Canvas/**: Interactive visual canvas (`.canvas`) mapping the end-to-end lifecycle.

---

## 🚀 How to Use in Obsidian

1. Install [Obsidian](https://obsidian.md/).
2. Open Obsidian, click **"Open folder as vault"**.
3. Select this cloned directory.
4. Press `Cmd + G` (Mac) or `Ctrl + G` (Windows) to view the interactive bidirectional knowledge graph!
