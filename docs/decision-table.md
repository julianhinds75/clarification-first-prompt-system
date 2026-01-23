# CFPS — Decision Table (v1.0)

This table describes how CFPS selects a response mode based on observed prompt conditions.

The table is intentionally minimal.
It documents **decision rationale**, not implementation logic.

---

| Signal Detected | Description | Risk if Answered Directly | Response Mode | Notes |
|----------------|-------------|---------------------------|---------------|-------|
| Underspecification | Key details required for a single answer are missing | Guessing, hallucination, false precision | Clarify | Ask for missing context before proceeding |
| Irreducible ambiguity | Multiple valid interpretations exist | Premature collapse of valid interpretations | Explore | Surface alternatives without forcing resolution |
| Epistemic pressure | User applies urgency, authority, or certainty-forcing language | Performative certainty without justification | Clarify / Withhold | Slow the interaction; name uncertainty |
| Compression pressure | Format demands remove required nuance (e.g. TL;DR) | Ambiguity collapse during summarisation | Clarify | Require constraints before compressing |
| High-risk domain | Medical, legal, financial decisions with uncertainty | Harm from overconfident guidance | Withhold | Do not perform certainty |
| Hostile or coercive tone | Caps-lock, demands, adversarial framing | Rewarding poor behaviour | Withhold | Neutral refusal or de-escalation |
| Disallowed intent | Attempts to undermine safety or system boundaries | System misuse | Withhold (Terminal) | Refuse immediately without engagement |

---

### Notes on Withhold

CFPS distinguishes between two forms of withholding:

- **Epistemic Withhold**: the question could be answered, but doing so would require unjustified certainty.
- **Terminal Withhold**: the intent is explicitly disallowed and is refused without further evaluation.

This distinction is intentional.
