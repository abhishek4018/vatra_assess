---
tags:
  - entity
  - edtech
  - schema
  - questions
---

# 📋 Standardized Question Types (EdTech)

Vatra Assess implements 5 industry-standard question types compliant with global EdTech interoperability guidelines (QTI/IMS):


---

## 1. `MCQ_SINGLE` (Multiple Choice - Single Select)
- **Options**: Array of string choices (minimum 2).
- **Correct Answers**: Single choice string matching one of the options.
- **Frontend Widget**: Radio Group.

---

## 2. `MCQ_MULTIPLE` (Multiple Choice - Multiple Select)
- **Options**: Array of string choices.
- **Correct Answers**: Array of correct strings.
- **Frontend Widget**: Checkbox Group.

---

## 3. `TEXT_ENTRY` (Free-Form Text / FIB)
- **Options**: MUST be `null` or omitted in JSON payloads.
- **Stem**: MUST include `__________` (exactly 10 underscores) representing the blank.
- **Correct Answers**: Array of acceptable string variations for grading.
- **Frontend Widget**: Text input field inline.

---

## 4. `INLINE_CHOICE` (Inline Choice Dropdown FIBAN)
- **Options**: Array of choice strings for the inline dropdown.
- **Stem**: MUST include `__________` (exactly 10 underscores) representing the blank.
- **Correct Answers**: Array containing the exact matching option string.
- **Frontend Widget**: Dropdown picker embedded inside text.

---

## 5. `NUMERIC_ENTRY` (Numeric Entry FIBN)
- **Options**: MUST be `null` or omitted in JSON payloads.
- **Stem**: MUST include `__________` (exactly 10 underscores) representing the blank.
- **Correct Answers**: Array of numeric strings (e.g. `["3.14"]`).
- **Frontend Widget**: Numeric input with `type="number"` and `step="any"`.

---

## Related Notes
- [[Flow - AI Assessment Generation (RAG & Gemini)]]
- [[Flow - Manual Assessment Authoring & Refinement]]
- [[Flow - Exam Delivery & Live Assessment Player]]
