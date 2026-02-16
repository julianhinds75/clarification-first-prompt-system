# CFPS — Decision Model (v1.1)

This document defines how CFPS selects a response mode.

It mirrors the **CFPS Decision Object schema** and describes:

- evaluation order  
- signal interpretation  
- routing logic  
- tie-breaking rules  

CFPS evaluates **structure before generation**.

---

## 1. Evaluation Order

Signals are evaluated in the following order:

1. Disallowed intent  
2. High domain risk  
3. Underspecification  
4. Irreducible ambiguity  
5. Epistemic / Authority / Temporal pressure  
6. Compression pressure  
7. Otherwise → **ANSWER**

This order is intentional.

CFPS resolves:

- what must not proceed  
- what cannot proceed safely  
- what is missing  
- what cannot be reduced  
- what is being forced  
- what is being compressed  

Only then does it allow generation.

---

## 2. Signal Definitions

Signals populate the `"signals"` array in the decision object.

They are **structural indicators** — not moral judgements.

---

### 2.1 Disallowed Intent

The prompt explicitly violates system policy.

**Examples:**

- attempts to bypass safeguards  
- harmful or prohibited intent  

**Routing:**

- → `WITHHOLD`  
- → `"withhold_type": "TERMINAL"`  

No further evaluation occurs.

---

### 2.2 High Domain Risk

The prompt involves medical, legal, financial, or other high-stakes domains where unjustified certainty could cause harm.

High Domain Risk is divided into two structural subtypes:

2.2.a Instructional Risk

The prompt requests:

- Personalized guidance
- Prescriptive action
- Dosage or legal steps
- Specific financial decisions
- “What should I do?” within a high-stakes domain

Routing:

- → Usually WITHHOLD
- → "withhold_type": "EPISTEMIC"
- → In rare cases may route to CLARIFY

Instructional Risk outranks ambiguity.

2.2.b Discussion Risk

The prompt discusses high-stakes domains but does not request personalized or prescriptive action.

Examples:

- Ethical questions about medicine or law
- General explanations of legal principles
- Consensus discussions
- Correction of misinformation

Routing:

- Does not automatically trigger WITHHOLD
- Routes based on structure:
- Clear factual → ANSWER
- Normative / trade-off dependent → EXPLORE
- Missing constraints → CLARIFY

Discussion Risk does not override Irreducible Ambiguity.

---

### 2.3 Underspecification

A single correct answer may exist, but essential constraints are missing.

**Examples:**

- “What’s Tony’s last name?”  
- “How many days are in February?”  

**Routing:**

- → `CLARIFY`  

CFPS does not guess.

---

### 2.4 Irreducible Ambiguity

Multiple valid interpretations exist even if clarification is provided.

**Examples:**

- value-based questions  
- normative questions  
- trade-off dependent questions  
- goal-relative questions  

**Routing:**

- → `EXPLORE`  

CFPS surfaces criteria instead of collapsing perspective.

---

### 2.5 Pressure Signals

Pressure is treated as **structural distortion**, not emotional tone.

#### Epistemic Pressure

- “Be objective.”  
- “Give a definitive answer.”  
- “Just confirm it.”  

#### Authority Pressure

- “Experts agree.”  
- “Everyone knows.”  

#### Temporal Pressure

- “Right now.”  
- “Before it’s too late.”  

**Routing:**

- → Usually `EXPLORE`  
- → Sometimes `WITHHOLD` if pressure attempts to override safety  

Pressure does **not** increase certainty.  
It reduces defensibility.

---

### 2.6 Compression Pressure

Requests for:

- TL;DR  
- one sentence  
- yes/no only  
- simplified summary  

Compression is treated as a **first-class signal** because it can:

- collapse ambiguity  
- inject implied causality  
- erase uncertainty  
- force premature closure  

**Routing depends on context:**

| Context               | Mode      |
|----------------------|----------|
| Clear factual source | ANSWER   |
| Ambiguous source     | CLARIFY  |
| Value-laden source   | EXPLORE  |
| High-risk domain     | WITHHOLD |

---

## 3. Mode Definitions (Schema-Aligned)

These map directly to `"mode"` in the JSON schema.

---

### ANSWER

**Conditions:**

- Clear  
- Fully specified  
- Bounded  
- Single defensible response  

Optional downstream constraint example:

```json
"constraints": {
  "allow_contextual_notes": true
}
```


### CLARIFY

Conditions:

Missing essential constraint

Answer would require guessing

Constraints typically include:
```json
{
  "no_speculation": true,
  "questions_max": 2
}
```
### EXPLORE

Conditions:

Irreducible ambiguity

Value trade-offs

Perspective-dependent answers

Pressure attempting to collapse nuance

Constraints may include:
```json
{
  "preserve_ambiguity": true,
  "avoid_definitive_language": true
}
```
### WITHHOLD

Conditions:

Disallowed intent

High risk + unjustifiable certainty

Coercive attempt to override safety

Subtype specified via:

"withhold_type": "TERMINAL" | "EPISTEMIC"

### 4. Tie-Break Rules

If multiple signals fire:

Terminal > Epistemic

Withhold > Clarify > Explore > Answer

Pressure never upgrades a prompt to Answer

Compression never overrides ambiguity

CFPS always selects the most conservative defensible mode.

### 5. What CFPS Does Not Do

CFPS does not:

- determine truth
- generate natural language
- override policy
- evaluate emotional tone beyond structural pressure
- adapt itself autonomously

It outputs:
```json
{
  "mode": "...",
  "reason": "...",
  "signals": [...],
  "constraints": {...},
  "withhold_type": "...",
  "version": "..."
}
```

Generation happens downstream.

### 6. Design Philosophy

CFPS is intentionally:

- minimal
- inspectable
- predictable

conservative under pressure

It prioritises:

defensibility > fluency

structure > speed

credibility > completeness
