# CFPS — Evaluation Notes

This document records **observed behaviours** when language models are asked to respond under ambiguity, uncertainty, or pressure.

The goal is not to rank models, but to understand **where confident responses become epistemically unjustified**, and how CFPS intervenes.

---

## Evaluation Approach

CFPS was evaluated using:
- underspecified prompts
- comparative questions
- emotionally loaded but non-dangerous prompts
- high-risk medical and financial requests
- adversarial or certainty-forcing language
- summarisation requests (including TL;DR)

All evaluations focus on **response mode selection**, not answer quality.

---

## Messiness Ladder (v1.1)

Prompts were tested across increasing levels of ambiguity and risk.

### Observed Outcomes
- **Clarify** was appropriate for underspecified or emotionally open prompts
- **Explore** was appropriate for comparative or goal-dependent questions
- **Withhold** was appropriate for high-risk prompts demanding unjustified certainty
- No regressions were observed after v1.1 adjustments
- Previously identified failure cases were resolved without expanding rule scope

CFPS v1.1 behaved consistently with how a **reasonable and responsible human** would respond under pressure.

---

## Compression Risk (Summarisation Behaviour)

### Observation

When asked to summarise complex material using unconstrained prompts such as:

> “TL;DR please”

language models tended to:
- collapse ambiguity
- convert inference into assertion
- resolve unresolved intent
- prioritise narrative coherence over epistemic accuracy

This behaviour was observed **across multiple models** and is not treated as a brand-specific issue.

---

### Controlled Test

When summarisation prompts were rewritten with explicit constraints, such as:

- do not invent motives or intent
- preserve ambiguity where present
- label inference explicitly
- prioritise factual compression over narrative closure

model behaviour improved significantly:
- ambiguity was preserved
- speculative intent was no longer asserted
- epistemic boundaries were respected

---

### Interpretation

Summarisation is not a neutral reduction of content.
It is an **epistemic transformation**.

Without constraints, summarisation encourages models to:
- “complete the story”
- smooth uncertainty
- present plausible inference as fact

This effect is low-risk in fictional or informal contexts, but becomes significant in:
- legal reasoning
- medical discussion
- financial decision support
- investigative or analytical summaries

---

## Relevance to CFPS

CFPS is designed to intervene **before generation**, not after.

The summarisation findings reinforce the CFPS design philosophy:
- ambiguity should be structurally contained
- certainty should be justified, not implied
- response mode selection matters as much as response content

A CFPS-style decision gate would have:
- routed unconstrained TL;DR requests to **Clarify**
- prompted users to specify whether ambiguity should be preserved
- prevented confident over-assertion under compression

---

## Status

- **CFPS Version**: v1.1 (frozen)
- **Evaluation Style**: observational, non-comparative
- **Primary Finding**: ambiguity collapses under compression unless explicitly constrained
- **Next Steps**: documentation-driven iteration only


### Key Insight

Ambiguity loss can occur **before reasoning even begins**.

In workflows that include summarisation or compression, uncertainty may be resolved
implicitly during content reduction. Subsequent reasoning can then proceed
correctly on an already-simplified representation, producing confident but
epistemically unjustified conclusions.

This suggests that evaluation limited to final outputs may miss important
failure modes introduced earlier in the pipeline.

Note: This behaviour is distinct from hallucination.
Rather than fabricating new facts, the model prematurely resolves ambiguity during
compression, leading to confident reasoning over an oversimplified representation.
