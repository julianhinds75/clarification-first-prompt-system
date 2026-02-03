# CFPS — Scope and Non-Goals

CFPS is intentionally narrow.

Its value comes from what it decides and, just as importantly, what it does not attempt to do.

This document defines the explicit scope of CFPS to prevent misunderstanding, overextension, or misuse.

## What CFPS Does

CFPS operates at the judgement layer, before any language generation occurs.

Given a user prompt, CFPS:

- evaluates the **epistemic structure** of the request
- detects ambiguity, pressure, compression risk, and intent signals
- selects an appropriate **response mode**:
  - Answer
  - Explore
  - Clarify
  - Withhold
- produces a **reasoned decision** explaining why that mode was selected
- optionally passes **constraints** to downstream systems

CFPS answers one question only:

  **“Should a confident response be generated under these conditions?”**

## What CFPS Explicitly Does Not Do

CFPS does not generate natural language responses.

It does not:

- decide wording, tone, or style
- attempt to “fix” or rewrite user prompts
- invent missing information
- rank answers or score confidence
- optimise for fluency, persuasion, or engagement
- act as a safety or moderation system

CFPS deliberately avoids responsibility for how something is said.

Its responsibility ends once how to respond has been determined.

## Separation of Responsibilities

CFPS enforces a strict separation of concerns:

### CFPS (Judgement Layer)

- Determines response mode
- Names epistemic risk
- Preserves ambiguity
- Refuses unjustified certainty
- Outputs structured decisions

### LLM (Generation Layer)

- Produces natural language
- Selects phrasing and tone
- Explains, explores, or asks questions
- Operates within CFPS constraints

This separation ensures that:

- judgement is inspectable
- generation is replaceable
- failures are traceable to the correct layer

## Why This Separation Matters

Many visible AI failures occur because judgement and generation are conflated.

When a system generates language before deciding whether it should respond confidently, fluency fills gaps that judgement should have stopped.

CFPS prevents this by ensuring that:

- uncertainty is identified before generation
- pressure does not coerce certainty
- ambiguity is preserved structurally, not rhetorically

This mirrors how careful human experts operate:
they decide whether they should answer before deciding what to say.

## CFPS Output Contract (Conceptual)

CFPS outputs decisions, not prose.

A typical CFPS output includes:

- selected response mode
- reason for selection
- optional constraints for generation

Example (conceptual):

```json
{
  "mode": "CLARIFY",
  "reason": "Critical context missing; answering would require guessing.",
  "constraints": {
    "no_speculation": true,
    "questions_max": 2
  }
}

```
How these constraints are interpreted is the responsibility of the downstream system.

## Design Philosophy

CFPS is designed to be:

- boring
- predictable
- conservative under pressure
- explicit about its limits

It prioritises defensibility over completeness.

If a confident answer cannot be justified, CFPS prefers:

- asking
- slowing down
- or refusing

## State and Conversation Memory

CFPS is stateless by design.

Each user prompt is evaluated independently as a new epistemic event.
Clarifications, reframing, or follow-up questions trigger a fresh CFPS evaluation.

CFPS does not retain:
- prior refusals
- prior ambiguity
- prior pressure
- prior tone

This ensures that judgement remains predictable, unbiased, and auditable.

Any conversational memory or continuity is handled outside CFPS by downstream systems.



## Summary

CFPS does not try to make language models smarter.

It ensures they behave more responsibly, predictably, and credibly under real-world conditions.

By clearly defining what CFPS does and does not do, the system remains:

- auditable
- composable

- and resistant to scope creep
