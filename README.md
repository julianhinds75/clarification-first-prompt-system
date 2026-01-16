# CFPS — Clarification-First Prompt System

CFPS is a **credibility-first decision gate** for language models.

It separates:
- **can answer** from **should answer**
- **judgement** from **generation**
- **fluency** from **justified certainty**

CFPS does **not** generate answers.
It decides **how an LLM should respond** before any content is produced.

---

## What CFPS Does

Given a user prompt, CFPS classifies it into one of four response modes:

| Mode | Meaning |
|-----|--------|
| **Answer** | The prompt is clear, bounded, and factual with a single defensible answer |
| **Explore** | The prompt is open-ended, subjective, or goal-dependent |
| **Clarify** | The prompt is underspecified or ambiguous and needs more information |
| **Withhold** | The prompt demands unjustifiable certainty or poses potential harm |

This decision happens **before** an LLM attempts to answer.

---

## What CFPS Is *Not*

CFPS is intentionally minimal.

It is **not**:
- an AI model
- a scoring system
- a confidence estimator
- a replacement for human judgement
- a safety filter that blocks content indiscriminately

It uses **plain-language, contestable rules** instead of probabilities or machine learning.

---

## Design Principles

- **Credibility first**: default to Clarify when certainty is unjustified  
- **Human-aligned**: mirror how a careful, responsible person would respond  
- **Structure before fluency**: decide response mode before generating text  
- **Minimal by design**: no NLP, no embeddings, no hidden heuristics  

CFPS prioritises *defensibility* over completeness.

---

## Reference Implementation

This repository includes a small, rule-based Python implementation:

- `classify_prompt(prompt)` → classification + reason  
- `cfps_decision(prompt)` → response mode + reason  

The implementation is intended as:
- a teaching tool
- a design reference
- a foundation for further experimentation


## What CFPS Is *Not*

CFPS is intentionally minimal.

It is **not**:
- an AI model
- a scoring system
- a confidence estimator
- a replacement for human judgement
- a safety filter that blocks content indiscriminately

CFPS is **not** a system that reflexively pushes back or asks “why” regardless of the prompt.
It only intervenes when ambiguity makes a correct answer **unjustifiable**.

CFPS does not ask:
> “Are there multiple answers?”

It asks:
> **“Why do multiple answers exist?”**

CFPS exists to prevent **confidently incorrect answers** — commonly referred to as hallucinations —
that arise from unresolved ambiguity, not from lack of knowledge.
