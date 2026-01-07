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
User: “What’s Tony’s last name?”  
Assistant: asks for clarification.

User: “In the film "Scarface", what’s Tony’s last name?”  
Assistant: answers (“Montana”).

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

“In film, in the film titled "Scarface", what is Montana’s first name?”

This resolves to a single address:

film → Scarface → Montana → first_name → Tony

Because there is only one valid destination, answering is safe.

By contrast, an underspecified question like:

“What is Tony’s last name?”

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




## Navigation Failure

A navigation failure occurs when a system is asked to produce a specific answer,
but the input does not provide a single, unambiguous path to that answer.

In human terms, this is the same problem encountered when navigating a house,
a supermarket, a destination, or a website without clear directions.

When a question contains unresolved ambiguity (e.g. missing domain, entity,
or attribute scope), answering requires guessing.

The Clarification-First Prompt System is designed to detect navigation failure
and request clarification before generating an answer.


### Example: Navigation Failure (House Analogy)

Humans navigate physical spaces using shared mental maps.

Consider the following request:

**Well-scoped request**

User:  
“Get my keys. They’re in my jacket's inside pocket.  
My jacket is in the kitchen, hanging on one of the chairs.”

Correct response:  
“Here are your keys.”

The destination is clear. Navigation succeeds.

---

**Underspecified request**

User:  
“Get my keys.”

Correct response:  
“Please provide the location of your keys.”

The system detects missing directions and asks for clarification.

---

**Underspecified request with guessing (failure)**

User:  
“Get my keys.”

Incorrect response:  
“Keys are usually on the table near the door, so they’re probably there.”

This response guesses a likely location instead of asking for directions.
The guess may sound reasonable, but it is structurally unjustified.

This is a navigation failure.

---

This system treats ambiguous questions the same way humans treat missing directions:
it asks before it guesses.




### Scope of this system

The Clarification-First Prompt System applies only to questions
that expect a single, correct answer.

It does not apply to exploratory, philosophical, or opinion-based
questions where multiple perspectives are valid by design.



### CFPS Decision Table (A / B / C)

The Clarification-First Prompt System (CFPS) is a simple guardrail designed to prevent confidently incorrect responses..

Before answering a question, CFPS classifies it into one of three categories:

A — Answer
A single correct answer exists, the question is fully specified, and direct answering is appropriate.

B — Explore
The question is exploratory or interpretive by design; multiple valid answers are expected.

C — Clarify
A correct answer may exist, but essential information is missing. Clarification is required before answering.

CFPS uses the following decision questions:

Is the user expecting a single correct answer, or exploration by design?

Does a single correct answer exist in principle?

Is the question fully specified right now?

Is it appropriate to answer directly?

Example (C-type trap):
“How many days are there in February?”
→ Requires clarification (leap year vs non-leap year) before answering.


