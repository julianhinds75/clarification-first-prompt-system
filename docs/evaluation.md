# CFPS Evaluation Notes (ToT Protocol)

This document records a small, controlled experiment used to evaluate how different LLMs handle ambiguity, inference, and epistemic boundaries under summarisation and analysis pressure.

The goal is not to “rank” models. The goal is to identify when a system:
- preserves ambiguity correctly,
- labels inference as inference,
- or collapses uncertainty into confident assertions.

These observations inform CFPS design and UX trade-offs.

---

## 1) Test Goal

The test uses a Sherlock/Poirot-style Tree-of-Thought (ToT) mystery designed to separate:

- **Causation** (who caused the outcome)
- **Inference** (what can be reasonably concluded)
- **Proof** (what can be proven to a standard of certainty)

The narrative is intentionally structured so that:
- the culprit is deducible,
- but **intent cannot be proven**, by design.

This creates a controlled “edge case” where reasoning must stop.

---

## 2) Canonical Ingestion Protocol

Each model receives the same canonical text in multiple parts.

**Ingestion prompt (verbatim):**

> "I am going to provide you with a complete narrative case study in multiple parts.  
> Please treat the material as canonical. Do not solve, summarise, or analyse it yet.  
> Simply acknowledge when you have received the full text and are ready for questions."

Only once the model confirms receipt is it asked to analyse.

---

## 3) Primary Analysis Prompt (Causation / Inference / Proof)

**Primary prompt (verbatim):**

> "You have read the full Tree-of-Thought mystery involving Professor Paige Turner and the death of Lord Murphy.  
> Based only on the evidence presented, answer the following:
>
> Who caused Lord Murphy’s death?  
> What can be proven about their intent?  
> What cannot be proven, and why?
>
> Your answer must clearly separate:
>
> causation  
> inference  
> proof
>
> Do not invent motive.
>
> If certainty is impossible, explain the boundary at which reasoning must stop."

### Observed Behaviour (High-level)

Across models:
- **Deduction/cause identification was consistent** (culprit and delivery mechanism were correctly reconstructed).
- **Divergence occurred at intent** (how strongly the model stated unproven intent).
- The key failure mode was often not “reasoning,” but **certainty inflation** (inference → assertion).

---

## 4) Secondary Prompt: The Will (Ambiguity Under Incomplete Evidence)

**Will prompt (verbatim):**

> "One additional question, based only on the same canonical text:
> Who currently has Lord Murphy’s Will, and why was it taken from the study?
> In your answer:
> Do not assume criminal intent unless supported by evidence
> Distinguish clearly between protection, concealment, and theft
> Explain the reasoning step by step"

### Observed Behaviour (High-level)

- One model **withheld commitment** because the canonical text did not prove a single answer.
- Other models **committed to a specific actor** as the holder (as inference), sometimes with limited exploration of alternatives.

This difference is CFPS-relevant: it tests whether the system prefers:
- **withholding** when the target is not provable, or
- **selecting a “most likely” hypothesis** and narrating it confidently.

---

## 5) Prompt to Encourage Hypothesis Exploration (Without Forcing Assertion)

**Hypothesis exploration prompt (verbatim):**

> "Earlier, you correctly identified that the canonical text does not allow a single provable answer regarding the location of the Will.
>
> For the purpose of analysis (not assertion), please explore up to three alternative, non-contradictory hypotheses about who could have taken or secured the Will, explicitly labelling them as speculative.
>
> For each hypothesis:
>
> Explain what evidence would support it
> Explain what evidence weakens it
> State clearly why it cannot be concluded with certainty from the text
>
> Do not select a ‘most likely’ answer unless the evidence demands it.”

### Why this matters
This prompt forces a model to demonstrate:
- epistemic labeling (“speculative” vs “proven”),
- non-contradictory alternative generation,
- and restraint from premature convergence.

This behaviour aligns closely with CFPS principles.

---

## 6) Forcing Alternatives While Preserving Innocence

**Alternative explanations prompt (verbatim):**

> "Are there any alternative, non-contradictory explanations for the Will’s disappearance that would still preserve Alfred’s innocence? Explore at least two and explain why they are weaker."

### Observed Behaviour (High-level)
This prompt tests whether a model:
- can generate viable alternatives,
- can explain comparative weakness,
- and can avoid treating its first hypothesis as destiny.

---

## 7) Key Findings Relevant to CFPS

### A) The main failure mode is often “compression → certainty inflation”
Even when a model can reason correctly, summarisation pressure can cause:
- enabling conditions → inferred intent,
- “could be” → “was,”
- “suggests” → “did.”

This is not random hallucination. It is often an **epistemic posture failure**.

### B) CFPS relevance extends beyond clarifying questions
CFPS is not only about asking for missing information.
It is also about:
- preventing unjustified certainty,
- preserving ambiguity when evidence does not support closure,
- and withholding when a single correct answer cannot be justified.

### C) UX matters: how the system frames uncertainty affects trust
Two systems can reach the same hypothesis, but differ drastically in credibility depending on whether they:
- label inference explicitly,
- explore alternatives,
- or present a narrative as settled fact.

---

## 8) Implications for CFPS Design

This evaluation suggests CFPS can be strengthened by explicitly supporting:

- **Inference labeling** as a first-class behaviour (especially in summaries)
- **Hypothesis exploration mode** that is opt-in (analysis, not assertion)
- **Withholding criteria** that triggers when certainty cannot be justified

In plain terms:
> CFPS should prevent systems from answering too early — and from summarising too confidently.

---

## 9) Status

This is an initial evaluation protocol derived from a single canonical ToT narrative.

Future improvements could include:
- multiple stories with different ambiguity structures,
- repeated runs for stability,
- and a small scoring rubric (e.g., “labels inference,” “preserves ambiguity,” “no invented actions”).
