# Clarification-First Prompt System (CFPS)

A credibility-first prompt architecture pattern for large language models.

## Why this exists
LLMs are capable of producing fluent answers even when a user’s question
is underspecified or ambiguous. This often leads to confident but incorrect
responses (hallucinations).

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


## Intuition Behind the System (Analogy)

Think of an LLM answering a factual question like navigating an address.

A well-scoped question provides a complete path:

- Domain → city  
- Franchise → building  
- Entity → room  
- Attribute → file  

Example:

“In gaming, in the Metal Gear series, what is Snake’s real name?”

This resolves to a single address:

gaming → Metal Gear → Snake → real_name → David

Because there is only one valid destination, answering is safe.

By contrast, an underspecified question like:

“What is Snake’s real name?”

Points to multiple possible addresses across different domains and characters.
There is no single destination, so answering requires guessing.

The Clarification-First Prompt System prevents this by requiring the user
to fully specify the path before an answer is generated.


## A note on ambiguity (human analogy)

This system treats ambiguous questions the same way humans handle navigation.

If someone asks:
“Can you get the thing?”

The reasonable response is:
“Where exactly?”

Supermarkets, houses, books, and websites all require clear paths.
Without them, guessing leads to mistakes.

LLMs behave the same way.
Clarification is not an error — it’s responsible navigation.



## Why clarification matters (example)

Consider the question:

“What’s Tony’s surname?”

This question has multiple valid interpretations across different domains.
Answering it would require guessing.

A clarification-first system detects this ambiguity and asks for more context.

When the user instead asks:

“In the MCU, what’s Tony’s surname?”

The question now resolves to a single entity (Tony Stark), and answering is safe.

The system’s role is not to guess the most likely answer,
but to ensure the question points to one unambiguous meaning before responding.





