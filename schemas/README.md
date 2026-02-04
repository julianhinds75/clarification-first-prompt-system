# CFPS Decision Schema

This schema defines the structured output produced by CFPS
before any language generation occurs.

It is a contract between:
- the CFPS judgement layer
- downstream generation systems (e.g. LLMs, agents, tools)

The schema ensures that CFPS decisions are:
- machine-parseable
- human-auditable
- versioned and explicit

CFPS produces decisions, not prose.
