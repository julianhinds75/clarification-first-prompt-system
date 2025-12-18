# Clarification-First Prompt System (CFPS)

A credibility-first prompt architecture pattern for large language models.

## Why this exists
LLMs are capable of producing fluent answers even when a user’s question
is underspecified or ambiguous. This often leads to confident but incorrect
responses (known as hallucinations).

This project demonstrates a prompt architecture pattern that prevents
ambiguous factual questions from being answered by requiring clarification
before generation.

## The core idea
Before answering a question that expects a single correct answer, the system
checks whether the request resolves to one unambiguous interpretation.

If it does not, the system asks a clarification question instead of guessing.

Correctness and credibility are prioritised over response speed.

## What this demonstrates
- ambiguity detection
- judgment about when NOT to answer
- clarification as a system feature, not a failure
- credibility-first AI behaviour
- human–AI interface design

## Example
User: “What’s David’s code name?”  
Assistant: asks for clarification.

User: “In Metal Gear, what’s David’s code name?”  
Assistant: answers (“Snake”).

## Status
Version 1.0 — initial system prompt and behavioural tests.
