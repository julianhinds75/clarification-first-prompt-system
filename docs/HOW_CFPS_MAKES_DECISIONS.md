# How CFPS Makes Decisions (Human Overview)

CFPS does not generate answers.

It decides **how** a system should respond *before* any language is produced.

This document explains that process in plain terms.

---

## The Core Idea

Before responding to a user, CFPS asks one question:

> **“Is it responsible to generate a confident answer under these conditions?”**

Everything else exists to support that decision.

---

## The Decision Comes First

CFPS always selects **one response mode**:

- **ANSWER**  
  A confident response is justified.

- **CLARIFY**  
  Critical information is missing.

- **EXPLORE**  
  The topic requires discussion, not resolution.

- **WITHHOLD**  
  A confident answer would be misleading or unsafe.

This decision is made **before** wording, tone, or explanation.

---

## How CFPS Decides (Conceptually)

CFPS looks at the *shape* of the prompt, not just its topic.

It considers factors such as:

- Is key context missing?
- Is the user forcing a binary answer onto a complex issue?
- Is there pressure to respond quickly or decisively?
- Would a confident answer collapse real uncertainty?
- Could a misleading answer cause harm?

CFPS does **not** try to “fix” the prompt.  
It decides whether a confident response is justified.

---

## A Simple Example

**User prompt:**

> “Just answer yes or no: should companies mandate return to office?”

**CFPS reasoning (simplified):**

- The issue depends on role, industry, culture, and constraints.
- A yes/no answer would erase valid alternatives.
- The user is applying compression pressure.

**CFPS decision:**

> **WITHHOLD**  
> A confident binary answer would be misleading.

The language model may still respond — but only within that constraint.

---

## Separation of Responsibilities

CFPS and the language model have different jobs.

### CFPS (Judgement Layer)
- Decides whether certainty is justified
- Preserves ambiguity when needed
- Refuses forced conclusions

### Language Model (Generation Layer)
- Chooses wording and tone
- Explains, explores, or asks questions
- Operates within CFPS constraints

This separation ensures:
- decisions are inspectable
- failures are traceable
- fluency cannot override judgement

---

## Why This Matters

Many AI failures happen because systems generate language
**before** deciding whether they should.

CFPS reverses that order.

It ensures:
- restraint before fluency
- judgement before explanation
- credibility under pressure

---

## What This Document Is (and Is Not)

This is a **conceptual overview**, not a technical specification.

Internal signal labels, thresholds, and schemas exist for:
- auditing
- consistency
- system integration

They are intentionally hidden here.

CFPS is designed to be understandable without technical expertise.
