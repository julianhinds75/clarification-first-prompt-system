# CFPS v1.1 — Version Freeze

This document formally freezes **CFPS v1.1**.

The purpose of this freeze is to:
- clearly define scope
- prevent silent feature creep
- make design decisions explicit and defensible
- establish a stable baseline for future iterations

CFPS v1.1 is considered **complete**.

---

## What CFPS v1.1 Is

CFPS v1.1 is a **credibility-first decision gate** that operates *before* language model generation.

Its sole responsibility is to decide **how an LLM should respond**, not *what* it should say.

CFPS v1.1:
- separates judgement from generation
- prioritises epistemic restraint over fluency
- treats pressure and compression as first-class signals
- behaves like a reasonable, responsible human under uncertainty

---

## Included Capabilities (v1.1)

CFPS v1.1 explicitly supports:

- Response mode selection:
  - **Answer**
  - **Explore**
  - **Clarify**
  - **Withhold**

- Detection and handling of:
  - underspecification
  - irreducible ambiguity
  - epistemic pressure
  - temporal and authority pressure
  - compression risk (e.g. TL;DR as failure mode)

- Distinction between:
  - **Epistemic Withhold** (restraint under uncertainty or pressure)
  - **Terminal Withhold** (explicitly disallowed intent)

- Transparent, rule-based decisioning:
  - no embeddings
  - no probabilistic scoring
  - no hidden heuristics

---

## Explicit Non-Goals (v1.1)

CFPS v1.1 intentionally does **not** attempt to:

- generate answers or content
- evaluate answer correctness
- optimise for model performance
- replace safety or moderation systems
- detect or defeat jailbreaks as a primary objective
- infer user intent beyond what is expressed in the prompt
- act as a policy engine or compliance framework

Requests that express explicitly disallowed intent are routed directly to **Terminal Withhold** and are not evaluated further.

---

## Design Philosophy (Locked)

The following principles are considered **stable** in v1.1:

- Silence and restraint are valid outcomes
- Pressure does not justify certainty
- Brevity must not destroy credibility
- Politeness does not dilute intent
- Indirection does not change disallowed behaviour

These principles are not under active revision for this version.

---

## What Comes Next

Future versions of CFPS may explore:
- orchestration and composition
- structured outputs and schemas
- expanded evaluation and stress testing
- integration into larger AI systems

Any such changes will occur under a new version and will not retroactively alter CFPS v1.1.

---

## Status

- **Version**: CFPS v1.1
- **State**: Frozen
- **Change Policy**: Documentation-only clarifications permitted; no behavioural changes
- **Next Planned Phase**: Composition & orchestration (v1.2+)
