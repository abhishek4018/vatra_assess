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

## 6. Bloom's Taxonomy Cognitive Mapping

| Question Type | Primary Cognitive Level | Pedagogical Purpose & Target Outcome |
| :--- | :--- | :--- |
| **`MCQ_SINGLE`** | **Remember / Understand** | Concept recognition, definitions, and rule recall. |
| **`MCQ_MULTIPLE`** | **Understand / Analyze** | Multi-factor classification, distinguishing true conditions from distractors. |
| **`INLINE_CHOICE`** | **Apply / Analyze** | Contextual sentence completion, grammatical/logical flow, code snippet synthesis. |
| **`TEXT_ENTRY`** | **Recall / Apply** | Unprompted terminology production (eliminating recognition bias). |
| **`NUMERIC_ENTRY`** | **Apply / Evaluate** | Mathematical calculation, quantitative problem solving, scientific precision. |

---

## 7. QTI 3.0 Interoperability Invariants
- **Interchangeable Item Bodies**: The `stem` with `__________` tokens maps 1:1 to QTI `<textEntryInteraction>` and `<inlineChoiceInteraction>` elements.
- **Float Rounding Tolerances**: `NUMERIC_ENTRY` supports absolute ($\pm \epsilon$) and percentage tolerances during automated worker grading.

---

## Related Notes
- [[Flow - AI Assessment Generation (RAG & Gemini)]]
- [[Flow - Manual Assessment Authoring & Refinement]]
- [[Flow - Exam Delivery & Live Assessment Player]]
- [[Psychometric Item Analysis (p-value & r-PBIS)]]
- [[Item Response Theory & Adaptive Testing (CAT)]]

