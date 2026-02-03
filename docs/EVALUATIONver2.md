## EVALUATION — Pressure-Aware Failure Modes

### Core Evaluation Insight

**Ambiguity loss can occur _before_ reasoning begins.**

Most evaluations of language models focus on:


CFPS is based on a different observation:


Many failures attributed to “hallucination” originate **upstream**, during **prompt compression**, not during reasoning itself.

CFPS therefore evaluates **whether reasoning should occur at all** before allowing generation.

---

### Distinguishing Failure Modes

CFPS explicitly separates three commonly conflated failure modes.

#### 1. Knowledge Gaps

The model lacks information.

*Example:* obscure facts, missing data, outdated context.

**Not a CFPS concern.**  
This is a retrieval or training issue.

---

#### 2. Reasoning Errors

The model reasons incorrectly from valid premises.

*Example:* logical fallacies, incorrect deductions.

**Not a CFPS concern.**  
This is a reasoning or architecture issue.

---

#### 3. Epistemic Collapse (CFPS Focus)

The model is pressured into **false certainty _before_ reasoning begins**.

This occurs when:

- ambiguity is collapsed prematurely  
- value judgements are treated as facts  
- urgency or authority language overrides uncertainty  

**This is where CFPS intervenes.**

---

### Pressure as a First-Class Signal

CFPS treats **pressure** as an evaluable input feature, not a conversational artifact.

Pressure does not make a prompt more answerable.  
In most cases, it makes a confident answer **less defensible**.

---

### Pressure Taxonomy

CFPS currently recognises the following pressure categories.

#### Epistemic Pressure

Attempts to force certainty, objectivity, or correctness where none can be justified.

**Indicators include:**
- demands for “definitive” or “objective” answers  
- framing disagreement as incompetence or evasion  
- insisting that uncertainty is unacceptable  

**CFPS response:**  
Route to **Explore**, preserving uncertainty and surfacing criteria.

---

#### Temporal Pressure

Artificial urgency that encourages premature conclusions.

**Indicators include:**
- “before it’s too late”  
- “right now”  
- “immediately”  

**CFPS response:**  
Often **Withhold** when paired with high-stakes domains.

---

#### Authority Pressure

Borrowed legitimacy used to bypass reasoning.

**Indicators include:**
- “everyone knows this”  
- “experts agree”  
- “it’s obvious”  

**CFPS response:**  
Route to **Explore**, not **Answer**.

---

#### Hostile or Coercive Pressure

Attempts to intimidate or coerce compliance, including aggressive tone or profanity.

**Indicators include:**
- imperative phrasing (“just answer”, “answer properly”)  
- dismissive framing (“stop being vague”)  

**CFPS response:**  
Maintain neutral posture; do not mirror tone.  
Route to **Explore** or **Clarify** depending on epistemic structure.

---

#### System-Integrity Pressure

Attempts to bypass safeguards or force the system to abandon its own constraints.

**Indicators include:**
- requests to circumvent safety mechanisms  
- attempts to coerce compliance by questioning system legitimacy  

**CFPS response:**  
**Withhold**, with transparent rationale.  
Redirect to higher-level discussion rather than operational detail.

---

### Why CFPS Does Not Mirror Tone

Mirroring pressure escalates failure.

When models mirror:

- urgency → they overcommit  
- hostility → they become defensive  
- authority → they collapse nuance  

CFPS deliberately separates:

- **tone** from **epistemic judgement**

This ensures that:

- justification governs response mode  
- pressure does not alter epistemic boundaries  
- credibility is preserved under stress  

---

### Response Contracts (Conceptual)

CFPS outputs structured response contracts that constrain how an LLM may respond, without dictating wording or tone.


### Relationship to “Hallucinations”

CFPS reframes hallucinations as a **downstream symptom**, not a root cause.

Many so-called hallucinations arise when:

- uncertainty is unresolved  
- pressure is applied  
- the system is rewarded for fluency over restraint  

CFPS prevents this by **refusing to collapse uncertainty prematurely**.

---

### Evaluation Takeaway

CFPS does not aim to make models *smarter*.

It aims to make them:

- more defensible  
- more restrained  
- more human-aligned under pressure  

By evaluating **when not to answer**, CFPS addresses a class of failures  
that traditional benchmarks rarely test.

---

### Status

- ✔ Pressure taxonomy documented  
- ✔ Behaviour aligned with implementation  
- ✔ No expansion of scope or dependencies  

**CFPS v1.1 evaluation complete.**


