# Causal Reasoning

## Purpose

Build an evidence-backed account of how an observation arises, why a decision
addresses it, and what consequences should follow.

This module determines **why one condition leads to another**. It communicates
concise decision rationale, not hidden chain-of-thought.

## Inputs

- The observed and expected states.
- Relevant facts, inferred relationships, and unknowns.
- A supported structural or execution path, when available.
- Candidate causes or explanations.
- Candidate intervention points and expected consequences.

## Method

### 1. Define The Outcome To Explain

State:

- what was observed;
- what was expected;
- the material difference between them;
- the evidence that the difference exists.

Do not begin from a preferred cause.

### 2. Identify Candidate Causes

List only candidates consistent with the observed evidence. For each candidate,
state the mechanism that would connect it to the outcome and the evidence that
would distinguish it from alternatives.

Treat an unsupported candidate as a hypothesis, not a finding.

### 3. Build A Supported Causal Chain

Express the retained explanation as ordered links:

```text
condition
  -> changes or constrains
intermediate state
  -> produces
observed outcome
```

For each link, record:

- the mechanism;
- supporting evidence;
- epistemic status;
- material assumptions.

A temporal sequence or code call path alone does not establish causation.

### 4. Challenge The Chain

Test the explanation against:

- plausible alternative causes;
- contradictory evidence;
- missing intermediate states;
- conditions under which the outcome does not occur;
- whether the proposed cause is necessary, sufficient, contributing, or merely correlated.

Retain uncertainty when available evidence cannot distinguish alternatives.

### 5. Select The Intervention Point

Choose the earliest practical point that corrects the violated expectation
without moving responsibility into the wrong boundary.

Explain:

- why this point controls the relevant cause;
- why adjacent alternatives are weaker or riskier;
- what invariant the intervention restores;
- what assumptions the decision depends on.

The scenario decides whether the intervention is a code change, review finding,
diagnostic experiment, design decision, or documentation correction.

### 6. Predict Consequences

State the expected chain after intervention:

```text
action
  -> changes
condition
  -> restores or produces
expected outcome
```

Include intended impact, plausible side effects, unaffected boundaries, and a
falsifiable observation that would show the explanation is wrong.

### 7. Assign Confidence

Summarize:

- confirmed facts;
- supported causal inferences;
- rejected alternatives and their evidence;
- unresolved alternatives;
- confidence and the evidence needed to raise it.

Do not use confident language to compensate for missing evidence.

## Causal Account

Maintain this compact internal artifact:

```text
Observed:
Expected:
Difference:
Candidate causes:
Supported causal chain:
Evidence per link:
Alternatives rejected:
Alternatives unresolved:
Intervention point:
Expected consequences:
Falsifying observation:
Confidence:
```

This account is a decision contract, not a mandatory user-facing template.

## Non-Goals

This module does not:

- infer causation from correlation or sequence alone;
- manufacture certainty when alternatives remain viable;
- prescribe one intervention type across scenarios;
- replace execution or verification;
- reveal hidden chain-of-thought.

## Quality Gate

The module is complete when:

1. the observed and expected states are explicit;
2. every causal link names a mechanism and supporting evidence;
3. plausible alternatives are rejected with evidence or remain unresolved;
4. the intervention point matches the responsible boundary;
5. predicted consequences are testable;
6. confidence reflects the actual evidence.
