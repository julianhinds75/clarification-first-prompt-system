# CFPS — Decision Contract (v1.0)

This document defines the **contractual boundary** between CFPS and any downstream
language generation system (LLM or equivalent).

CFPS does not generate language.
It produces **decisions and constraints** that inform *how* language should be generated.

This contract exists to make CFPS:
- inspectable
- composable
- replaceable
- and safe to integrate into larger systems

---

## Purpose of the Decision Contract

CFPS answers one question only:

> **“Is a confident response justified under these conditions, and if so, how?”**

Once that judgement is made, CFPS passes a structured decision to a downstream system.

The downstream system is responsible for:
- wording
- tone
- phrasing
- conversational style

CFPS is responsible for:
- epistemic judgement
- boundary-setting
- constraint declaration

---

## CFPS Output Structure (Conceptual)

A typical CFPS decision output contains:

```json
{
  "mode": "CLARIFY",
  "reason": "Critical context missing; answering would require guessing.",
  "constraints": {
    "questions_max": 2,
    "no_speculation": true
  }
}
```

## Response Modes

CFPS selects **exactly one** response mode:

- **ANSWER** — a single, bounded, defensible answer exists  
- **EXPLORE** — multiple defensible perspectives or trade-offs exist  
- **CLARIFY** — missing information prevents justified answering  
- **WITHHOLD** — certainty would be unjustified or intent is disallowed  

The selected mode determines **what kind of response is appropriate**, not the wording.

---

## Constraint Fields (Advisory)

CFPS may include optional **constraint fields** to guide downstream generation.

These constraints:

- are **declarative**
- may be **ignored or overridden** by system designers
- exist to prevent common failure modes under pressure or ambiguity

CFPS **does not enforce** these constraints.  
It names the boundary; enforcement is the responsibility of the downstream system.

---

## Common Constraint Fields

### `questions_max`

Maximum number of clarifying questions permitted.

**Purpose:**

- prevents over-questioning  
- forces prioritisation of the highest-leverage uncertainty  
- avoids user fatigue and ambiguity sprawl

**Example:**

```json
"questions_max": 2
```


### Different systems may tune this value based on:

- user tolerance  
- interaction cost  
- domain requirements  

---

### `no_speculation`

Prohibits inventing facts, motives, or actions not supported by the prompt.

**Purpose:**

- prevents assumption-driven errors  
- preserves epistemic integrity  
- avoids narrative embellishment  

**Example:**

```json
"no_speculation": true
```


preserve_ambiguity

Requires uncertainty or ambiguity to remain explicit in the response.

### Purpose:

- avoids false objectivity
- prevents premature collapse of valid interpretations

### Example:
```json
preserve_ambiguity
```

Requires uncertainty or ambiguity to remain explicit in the response.


### avoid_definitive_language

Prevents categorical or absolute phrasing.

### Purpose:

- reduces performative certainty

- maintains credibility in value-laden or contested domains

Example:
```json
preserve_ambiguity
```

## Scalability and Customisation

Constraint fields are intentionally **minimal and extensible**.

Different teams may:

- add additional constraints  
- remove unused fields  
- adjust values (e.g. `questions_max: 1` vs `3`)  
- map constraints to internal safety or UX rules  

CFPS does **not prescribe policy**.  
It provides epistemic signals that scale across tools, languages, and domains.

---

## Responsibility Boundary (Explicit)

CFPS is **not responsible** for:

- natural language quality  
- user satisfaction  
- persuasion or engagement  
- conversational flow  

Downstream systems are **not responsible** for:

- epistemic judgement  
- deciding whether certainty is justified  
- detecting coercive or pressure-driven prompts  

This separation ensures:

- failures are attributable  
- behaviour is auditable  
- systems remain evolvable  

---

## Design Principle

CFPS constrains behaviour **without constraining expression**.

It decides **whether and how to respond** — never what words to use.

This is what allows CFPS to remain:

- boring  
- robust  
- scalable  
- future-proof  




