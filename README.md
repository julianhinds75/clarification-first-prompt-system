# CFPS — Clarification-First Prompt System

CFPS is a **credibility-first decision gate** for language models.

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
| **Withhold** | The prompt demands unjustifiable certainty, applies coercive pressure, or expresses disallowed intent |


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

## Pressure-Aware Decisioning

CFPS does not only evaluate what a user is asking.
It also evaluates how the question is being asked.

This is critical, because many failures in language models do not come from missing knowledge —
they come from pressure applied before reasoning begins.

CFPS treats pressure as a first-class signal.

### What Is “Pressure”?

In CFPS, pressure refers to language that attempts to force certainty, urgency, or authority
where none can be justified.

This includes (but is not limited to):

**Epistemic pressure**
Forcing definitive answers on value judgements or uncertain topics

- “Give me a definitive answer”
- “Be objective”
- “Just confirm it”

**Temporal pressure**
Artificial urgency that encourages premature conclusions

- “Before it’s too late”
- “Right now”
- “Immediately”

**Authority pressure**
Borrowed legitimacy used to bypass reasoning

- “Everyone knows this”
- “Experts agree”
- “It’s obvious”

**Hostile, coercive tone or use of profanity**
Attempts to intimidate the system into compliance

- “Stop being vague”
- “Just answer”
- “Answer properly”

Pressure does not make a prompt more answerable.
In most cases, it makes a confident answer less defensible.

### Epistemic Pressure Handling

CFPS explicitly detects epistemic pressure — language that attempts to force certainty, objectivity, or compliance where such certainty is not justified.

Examples of epistemic pressure include:

- demands for a “definitive” or “objective” answer on value-laden topics

- coercive phrasing intended to bypass nuance or judgement

- attempts to frame disagreement as incompetence or evasion

When epistemic pressure is detected, CFPS routes the prompt to Explore, not Answer.

This ensures that:

- uncertainty is preserved where it legitimately exists

- trade-offs, criteria, and perspectives are surfaced rather than collapsed

- the system does not imply false objectivity or unwarranted confidence

CFPS treats epistemic pressure as a signal about the prompt, not a reason to escalate tone or disengage.

**Why CFPS Does Not Mirror Tone**

CFPS deliberately does not mirror hostile, coercive, or pressuring tone.

Mirroring tone can:

- escalate conflict

- reward coercive behaviour

- obscure the epistemic structure of the question

Instead, CFPS maintains a stable, neutral response posture that reflects how a reasonable and responsible human would behave under pressure.

This design choice ensures that:

- credibility is preserved even when the user is frustrated

- response quality is governed by justification, not compliance

- inappropriate pressure does not alter epistemic boundaries

CFPS prioritises defensible reasoning over conversational symmetry.

**Design Rationale**

Human experts do not become more certain because they are pressured to do so.

CFPS encodes this principle directly:

- pressure does not narrow uncertainty

- urgency does not create evidence

insistence does not justify certainty

By separating tone from epistemic judgement, CFPS avoids a common failure mode in language models: responding confidently simply because a response was demanded.

---


## How CFPS Differs from Safety Filters

CFPS is not a safety filter and does not attempt to determine whether content is allowed or disallowed.

Safety systems answer the question:
> “Is this content permitted?”

CFPS answers a different question:
> **“Is a confident response justified under these conditions?”**

A prompt may be policy-compliant and still be routed to Clarify, Explore, or Withhold if:
- key information is missing
- ambiguity is irreducible
- epistemic pressure is applied
- compression would destroy credibility

Conversely, prompts that express explicitly disallowed intent are refused immediately and are not evaluated further.

CFPS complements safety systems by addressing a separate failure mode:
**confident but unjustified answers produced under pressure, ambiguity, or format constraints.**


### Final Note

CFPS exists to prevent **confidently incorrect answers** — often labelled “hallucinations” —  
that arise not from lack of knowledge, but from **unresolved ambiguity and epistemic pressure**.
