# CFPS — Clarification-First Prompt System

CFPS is a **credibility-first decision layer** for language models.

It separates:

- can answer from should answer  
- judgement from generation  
- fluency from justified certainty  

CFPS does **not** generate responses.  
It determines how an LLM should respond *before* any content is produced.

---

## The Core Idea

Many visible AI failures do not stem from missing knowledge.

They arise when systems:

- collapse unresolved ambiguity  
- compress nuance into binary formats  
- respond under coercive or epistemic pressure  
- imply certainty without structural justification  

CFPS prevents this by making a decision **before generation begins**.

---

## Response Modes

For every prompt, CFPS selects **exactly one** mode:

| Mode     | Meaning                                      |
|----------|----------------------------------------------|
| Answer   | Clear, bounded, factual, defensible          |
| Explore  | Open-ended, subjective, value-dependent      |
| Clarify  | Underspecified or ambiguous                  |
| Withhold | Disallowed intent, high-risk prescriptive requests, or unjustifiable certainty |

This classification happens **prior to generation**.

---

## Pressure Awareness

CFPS treats epistemic pressure as a structural signal.

**Examples:**

- “Just answer yes or no.”  
- “Be objective.”  
- “Give a definitive answer.”  
- “Don’t hedge.”  

Pressure does not create evidence.

When pressure attempts to force certainty, CFPS routes the prompt to **Explore** or **Withhold**, preserving defensibility.

See `/docs/decision-model.md` for the full signal taxonomy.

---

## What CFPS Is Not

CFPS is not:

- an AI model  
- a moderation system  
- a probability estimator  
- a confidence scorer  

Safety systems ask:

> “Is this content allowed?”

CFPS asks:

> “Is a confident response justified under these conditions?”

It complements safety systems by addressing **epistemic failure** — not content policy.

---

## Design Principles

- Structure before fluency  
- Credibility over completeness  
- Pressure does not override uncertainty  
- Judgement is inspectable  
- Generation is replaceable  

CFPS prioritises **defensibility**.

---

## Reference Implementation

This repository includes a minimal rule-based Python implementation:

- `classify_prompt(prompt)`  
- `cfps_decision(prompt)`  

The implementation serves as:

- a design reference  
- a teaching artifact  
- a foundation for experimentation  

---

## Why This Matters

Human experts decide whether they should answer  
before deciding what to say.

CFPS encodes that discipline into LLM workflows.
