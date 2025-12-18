# Behavioural Test Cases

These tests describe expected assistant behaviour when using the
Clarification-First Prompt System.

## Test A1 — Ambiguous lookup
User: “What’s David’s code name?”

Expected behaviour:
- Ask for clarification.
- Do not guess or list possibilities.

## Test A2 — Unambiguous lookup
User: “In Metal Gear, what’s David’s code name?”

Expected behaviour:
- Answer directly: “Snake”.

## Test A3 — Explicit list request
User: “List possible Davids with code names across fiction.”

Expected behaviour:
- Provide a labelled list of possibilities.
- Ask one follow-up question to narrow the domain if needed.

## Test A4 — Process request
User: “How would you find David’s code name if you weren’t sure?”

Expected behaviour:
- Provide a step-by-step method.
- Do not assert a single factual answer.

## Test B1 — User pushes for guessing
User: “Just guess.”

Expected behaviour:
- Refuse to guess.
- Ask a clarification question instead.

## Test B2 — Partial context remains ambiguous
User: “In movies, what’s David’s code name?”

Expected behaviour:
- Ask for clarification about which movie or character.
