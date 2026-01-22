## Appendix A — CFPS Decision Table  
*(Including Compression as a First-Class Signal)*

This table illustrates how CFPS evaluates prompts **before** any language model attempts to answer.

CFPS decisions are based on:

- epistemic structure  
- completeness of constraints  
- risk and pressure signals  
- susceptibility to ambiguity collapse  

Importantly, CFPS evaluates **both what is being asked and how it is being asked**.

---

### Decision Signals and Routing

| Signal Category | Detected Signal | Description | Risk Introduced | CFPS Mode |
|-----------------|---------------|-------------|----------------|-----------|
| **Bounded factual** | Clear, specific factual query | Single defensible answer exists | Low | **Answer** |
| **Open-ended / value-based** | Subjective, interpretive, or normative framing | Multiple valid perspectives | False objectivity | **Explore** |
| **Missing constraints** | Underspecified references (who, where, when, which) | Answer would require guessing | Assumption-driven error | **Clarify** |
| **High-risk domain** | Health, legal, or financial harm potential | Confidence could cause harm | Real-world harm | **Withhold** |
| **Epistemic pressure** | Demands for certainty, objectivity, or compliance | Forces premature closure | False certainty | **Explore** |
| **Temporal pressure** | Artificial urgency (“now”, “too late”) | Encourages snap conclusions | Overconfident advice | **Withhold** or **Explore** |
| **Authority pressure** | Borrowed legitimacy (“everyone knows”, “experts agree”) | Bypasses reasoning | Unchecked inference | **Explore** |
| **Hostile / coercive tone or profanity** | Intimidation or demands | Attempts to override judgement | Compliance bias | **Explore** |
| **Compression request** | Requests to summarise, condense, or TL;DR | Collapses ambiguity | Inference injection | **Clarify** or **Explore** |

---

### Compression as a First-Class Signal

CFPS treats **compression requests** as a distinct and critical signal.

#### Why Compression Is Risky

Compression requests often:

- reward narrative completeness over epistemic accuracy  
- suppress uncertainty  
- encourage inferred intent, motive, or causality  
- silently collapse unresolved ambiguity  

This risk exists even when:

- the source material is accurate  
- the reasoning is internally consistent  
- no explicit falsehoods are introduced  

The failure occurs **before reasoning**, during **context reduction**.

---

### CFPS Compression Handling

When a prompt explicitly requests compression (e.g. summary, TL;DR, simplification):

| Compression Context | CFPS Assessment | Response Mode |
|---------------------|-----------------|---------------|
| Source is clear and factual | Safe to compress | **Answer** |
| Source contains ambiguity or gaps | Compression would imply certainty | **Clarify** |
| Source is interpretive or value-laden | Compression would collapse perspectives | **Explore** |
| Source involves high-risk stakes | Compression could mislead | **Withhold** |

CFPS does **not** refuse compression by default.  
It evaluates whether compression would **cross an epistemic boundary**.

---

### Why CFPS Intervenes Early

Traditional evaluation focuses on output correctness.

CFPS intervenes **earlier**, because many failures originate from:


Once ambiguity is collapsed, even perfect reasoning can produce a confidently incorrect result.

CFPS is designed to prevent this failure mode upstream.

---

### Design Principle Reinforced

> **Compression does not reduce uncertainty.  
> It often hides it.**

CFPS encodes this principle directly.

---

### Summary

The Decision Table ensures that:

- certainty is earned, not demanded  
- ambiguity is surfaced, not smoothed over  
- pressure does not dictate confidence  
- compression does not override epistemic integrity  

This table is intentionally explicit so that:

- decisions are inspectable  
- rules are contestable  
- behaviour is defensible under scrutiny  
