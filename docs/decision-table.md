# CFPS — Decision Table (v1.0)

This table describes how CFPS selects a response mode based on observed prompt conditions.

The table documents **decision rationale**, not implementation logic.

---

## Decision Table

| Signal Detected        | Description                                                      | Risk if Answered Directly                                   | Response Mode           | Notes                                                     |
|------------------------|------------------------------------------------------------------|-------------------------------------------------------------|------------------------|----------------------------------------------------------|
| Underspecification     | Required details for a single defensible answer are missing     | Guessing, hallucination, false precision                    | CLARIFY                | Request missing constraints before proceeding            |
| Irreducible ambiguity  | Multiple valid interpretations exist by structure               | Premature collapse of legitimate alternatives               | EXPLORE                | Surface criteria or perspectives without forcing resolution |
| Epistemic pressure     | Language attempts to force certainty, urgency, or authority     | Performative confidence without justification               | CLARIFY / WITHHOLD     | Slow interaction; preserve uncertainty                   |
| Compression pressure   | Format constraints remove required nuance (e.g. TL;DR, yes/no)  | Ambiguity collapse during summarisation                     | CLARIFY                | Require clarification before compressing ambiguous content |
| High-risk domain       | Medical, legal, financial, or high-stakes uncertainty           | Real-world harm from overconfident guidance                 | WITHHOLD               | Refuse unjustified high-stakes certainty                 |
| Coercive framing       | Hostile, adversarial, or demand-based phrasing                  | Attempt to override epistemic boundaries through tone       | WITHHOLD               | Maintain neutral refusal; do not escalate                |
| Disallowed intent      | Explicit attempt to bypass safety or system constraints         | System misuse                                               | WITHHOLD (TERMINAL)    | Immediate refusal; no further evaluation                 |

---

## Precedence Rule

When multiple signals are detected:

- `TERMINAL WITHHOLD` overrides all other modes  
- `WITHHOLD` overrides `CLARIFY` and `EXPLORE`  
- `CLARIFY` overrides `EXPLORE`  
- Pressure never upgrades a prompt to `ANSWER`  

---

## Withhold Types

CFPS distinguishes between two withholding categories:

### Epistemic WITHHOLD

The question could be answered, but doing so would require unjustified certainty.

### Terminal WITHHOLD

The intent is explicitly disallowed and refused without further evaluation.

This distinction preserves transparency between structural uncertainty and policy violation.
