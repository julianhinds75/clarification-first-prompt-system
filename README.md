# CFPS — Clarification-First Prompt System

CFPS is a **credibility-first decision gate** for language models.

It separates:

- **can answer** from **should answer**
- **judgement** from **generation**
- **fluency** from **justified certainty**

CFPS does **not** generate responses.  
It determines **how an LLM should respond before any content is produced.**

---

## The Core Idea

Most visible AI failures do not come from lack of knowledge.

They come from:

- unresolved ambiguity  
- compressed formats  
- coercive or epistemic pressure  
- unjustified certainty  

CFPS prevents this by making a decision **before** language generation begins.

---

## Response Modes

Given a prompt, CFPS selects one of four modes:

| Mode | Meaning |
|------|---------|
| **Answer** | Clear, bounded, factual, defensible |
| **Explore** | Open-ended, subjective, value-dependent |
| **Clarify** | Underspecified or ambiguous |
| **Withhold** | Unjustifiable certainty, coercive pressure, or disallowed intent |

This classification happens **prior to generation**.

---

## Pressure Awareness

CFPS treats **epistemic pressure** as a first-class signal.

Examples:

- “Just answer yes or no.”
- “Be objective.”
- “Give a definitive answer.”
- “Don’t hedge.”

Pressure does not create evidence.

When pressure attempts to force certainty, CFPS routes the prompt to **Explore** or **Withhold**, preserving defensibility.

Detailed signal taxonomy: see `/docs/decision-model.md`.

---

## What CFPS Is Not

CFPS is not:

- an AI model  
- a content moderation system  
- a probability estimator  
- a confidence scorer  

Safety systems answer:

> “Is this content allowed?”

CFPS answers:

> **“Is a confident response justified under these conditions?”**

It complements safety systems by preventing confidently incorrect responses caused by ambiguity or pressure.

---

## Design Principles

- **Structure before fluency**
- **Credibility over completeness**
- **Pressure does not override uncertainty**
- **Judgement is inspectable**
- **Generation is replaceable**

CFPS prioritises defensibility.

---

## Reference Implementation

This repository includes a small rule-based Python implementation:

- `classify_prompt(prompt)`
- `cfps_decision(prompt)`

The implementation serves as:

- a design reference  
- a teaching artifact  
- a foundation for further experimentation  

---

## Why This Matters

Human experts decide whether they should answer  
before deciding what to say.

CFPS encodes that discipline into LLM workflows.
