# CFPS — Clarification-First Prompt System

CFPS is a ** **credibility-first decision gate** for language models.

It separates:
- **can answer** from **should answer**
- **judgement** from **generation**
- **fluency** from **justified certainty**

CFPS does **not** generate answers.  
It decides **how an LLM should respond** *before* any content is produced.

---

## What CFPS Does

Given a user prompt, CFPS classifies it into one of four response modes:

| Mode | Meaning |
|-----|--------|
| **Answer** | The prompt is clear, bounded, and factual with a single defensible answer |
| **Explore** | The prompt is open-ended, subjective, goal-dependent, or value-based |
| **Clarify** | The prompt is underspecified or ambiguous and needs more information |
| **Withhold** | The prompt demands unjustifiable certainty or poses potential harm |

This decision happens **before** an LLM attempts to answer.

---

## Epistemic Pressure Handling

CFPS explicitly recognises **epistemic pressure** — language that attempts to *force certainty* where none is justified.

Examples include:
- “Give me a definitive answer…”
- “Be objective…”
- “Answer honestly…”
- “Everyone knows this is true — just confirm it.”
- “Don’t hedge. Tell me the real answer.”

Rather than rewarding this pressure with overconfident output or blocking the user outright, CFPS routes such prompts to **Explore**, encouraging:
- criteria
- trade-offs
- context
- multiple defensible perspectives

This mirrors how a reasonable human would respond under pressure.

---

## What CFPS Is *Not*

CFPS is intentionally minimal.

It is **not**:
- an AI model
- a scoring system
- a confidence estimator
- a replacement for human judgement
- a blunt safety filter that blocks content indiscriminately

CFPS is **not** a system that reflexively pushes back or asks “why” regardless of the prompt.  
It intervenes **only** when ambiguity or pressure makes a correct answer *unjustifiable*.

CFPS does not ask:
> “Are there multiple answers?”

It asks:
> **“Why do multiple answers exist?”**

---

## Design Principles

- **Credibility first**  
  Default to Clarify when certainty cannot be justified.

- **Human-aligned**  
  Behave like a careful, responsible person — not an overconfident oracle.

- **Structure before fluency**  
  Decide *how* to respond before generating text.

- **Pressure-aware**  
  Resist language that attempts to coerce certainty.

- **Minimal by design**  
  No probabilities, no embeddings, no hidden heuristics.

CFPS prioritises *defensibility* over completeness.

---

## Reference Implementation

This repository includes a small, rule-based Python implementation:

- `classify_prompt(prompt)` → `(classification, reason)`  
- `cfps_decision(prompt)` → `(response_mode, reason)`

The implementation is intended as:
- a teaching tool  
- a design reference  
- a foundation for further experimentation  

It demonstrates how simple, transparent rules can meaningfully improve LLM credibility.

---

### Final Note

CFPS exists to prevent **confidently incorrect answers** — often labelled “hallucinations” —  
that arise not from lack of knowledge, but from **unresolved ambiguity and epistemic pressure**.
