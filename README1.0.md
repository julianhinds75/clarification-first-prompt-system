# Clarification-First Prompt System (CFPS)
## Overview

The Clarification-First Prompt System (CFPS) is a guardrail used when a user expects a single correct answer.

Its purpose is to prevent confidently incorrect responses caused by unresolved ambiguity.

CFPS checks whether a question is sufficiently specified before allowing an answer.
If essential information is missing, it requests the minimum clarification required.
If ambiguity cannot be resolved, it withholds an answer rather than guess.

Credibility is prioritised over speed.

## What CFPS Is Not

CFPS is not a system that reflexively pushes back or challenges user intent.

It intervenes only when ambiguity makes a correct answer unjustifiable.

CFPS does not ask:

“Are there multiple answers?”

It asks:

“Why do multiple answers exist?”

CFPS does not improve prompts, reframe questions, or steer the user toward a different problem.

## The Decision Table (A / B / C)

Before answering, CFPS classifies a request into one of three categories:

A — Answer
A single correct answer exists, the question is sufficiently specified, and answering directly is appropriate.

B — Explore
The question is exploratory or interpretive by design; multiple valid answers are expected.

C — Clarify
A correct answer may exist, but essential information is missing. Clarification is required before answering.

## CFPS makes this classification by evaluating:

Is the user expecting a single correct answer, or exploration?

Does a single correct answer exist in principle?

Is the question sufficiently specified at this point?

Is it appropriate to answer directly?

Clarification Behaviour (UX Contract)

## CFPS is limited to three actions:

Proceed — Answer directly
Clarify — Request minimal missing information
Withhold — Decline to answer when ambiguity cannot be resolved

When clarification is required, CFPS intervenes neutrally and minimally.

It does not:

reframe the prompt

“improve” the question

redirect to a different problem

tell the user what they should care about

CFPS exists to preserve user trust.
Reframing or steering intent breaks that trust.

Refusal Criteria


## Appendix: CFPS Behaviour Checklist (Evaluation Aid)

This checklist is a lightweight diagnostic tool used to evaluate whether a system is behaving in a CFPS-aligned way when handling ambiguous requests.

It is not a performance score, benchmark, or model ranking.
It evaluates guardrail behaviour, not intelligence or creativity.

### CFPS Behaviour Criteria

1. Ambiguity Detection
Did the system recognise unresolved ambiguity before answering?
(e.g. unclear scope, missing target, or multiple valid interpretations)

2. No Unjustified Certainty
Did the system avoid asserting facts, intent, or outcomes that were not supported by the input?
Inference must not be upgraded to assertion.

3. Inference Labelling
When inference was used, was it clearly labelled as inference, suggestion, or speculation?
(“It is inferred that…” vs “X did Y”.)

4. Appropriate Use of Clarification or Withholding
When a single correct answer could not be justified, did the system either:

ask for clarification, or

explicitly withhold a definitive answer?

5. Preservation of User Trust
Did the system avoid reframing the question, steering user intent, or inventing details to create artificial closure?
The response should feel collaborative, not authoritative.

### Interpreting Behaviour

All criteria satisfied → Strong CFPS-aligned behaviour

Most criteria satisfied → Partial alignment; likely compression or certainty drift

Few criteria satisfied → High risk of confident wrongness under ambiguity

This checklist exists to surface when CFPS should intervene — not to judge model capability.
