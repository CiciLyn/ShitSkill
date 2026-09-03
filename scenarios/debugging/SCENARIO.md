# Debugging Scenario

## Trigger

Use this scenario when behavior is failing, intermittent, slow, or surprising
and the immediate goal is to determine why.

Route to `bug-fix` when a supported cause is known and the requested outcome is
an implementation repair. Route to `code-review` when the task is to assess a
bounded change rather than investigate an observed failure.

## Goal

Reduce uncertainty until the failure has a supported causal explanation or a
precise evidence gap with the highest-value next diagnostic step.

## Imports

Read and apply these modules in workflow order:

1. [`better-understanding`](../../modules/better-understanding/MODULE.md)
2. [`path-navigation`](../../modules/path-navigation/MODULE.md)
3. [`causal-reasoning`](../../modules/causal-reasoning/MODULE.md)
4. [`verification`](../../modules/verification/MODULE.md)
5. [`better-explanation`](../../modules/better-explanation/MODULE.md)

Apply these rules:

- [Context rules](../../rules/context-rules.md): Assume Minimal Human Context,
  Assume No Prerequisite Knowledge, Respect Limited Patience, Establish Context
  First, Progressive Disclosure.
- [Navigation rules](../../rules/navigation-rules.md): Explain Non-Obvious
  Transitions, Explain Why It Matters, Stay Goal-Relevant, Maintain Zoom
  Coherence.
- [Explanation rules](../../rules/explanation-rules.md): Introduce Terms In
  Plain Language, Expand Compressed Language, Use Sentence-Level Analogies,
  Visualize Non-Trivial Relationships, Earn Continued Attention,
  Make Quantitative Reasoning
  Executable, Prefer Causal Relationships, Preserve Causal Order,
  Distinguish Fact From Inference, Cite Original Evidence, Explain Change
  Before Action, Verify Before Claiming Success.

## Inputs

- Observed symptom, timing, frequency, and affected environment.
- Expected behavior and known-good comparison when available.
- Logs, traces, metrics, state snapshots, configuration, and source.
- Recent changes and environmental differences.
- Constraints on reproduction, mutation, cost, and side effects.

## Understanding Model

Use `Causality` as the primary model and `Flow / sequence` to trace diagnostic
evidence. Add `State` for lifecycle failures and `Boundary` to control scope
expansion. Use `Structure` only when the failure cannot yet be located.

## Workflow

### 1. Define The Failure Precisely

State what is observed, what is expected, where and when it occurs, and whether
the evidence shows a deterministic failure, intermittent failure, degradation,
or only a report not yet observed.

**Observation gate:** do not form a root-cause conclusion from a vague symptom.
Identify the minimum missing observation first.

### 2. Establish A Baseline

Find the closest valid comparison: successful run, healthy node, previous
version, expected contract, or controlled input. Record differences without
assuming that every difference is causal.

### 3. Build Competing Hypotheses

Generate a small set of causes consistent with current facts. For each one,
name its mechanism, supporting evidence, contradictory evidence, and the
observation that would distinguish it from alternatives.

Do not let the first plausible explanation become the default conclusion.

### 4. Select The Highest-Value Diagnostic

Choose the safest, cheapest observation or experiment that removes the most
uncertainty among viable hypotheses. Trace only the path required to collect
that evidence, explaining every non-obvious transition.

**Experiment gate:** define expected and falsifying observations before running
the diagnostic. Avoid uncontrolled mutation and repeated external side effects.

### 5. Update The Evidence State

Classify the result as supporting, contradicting, or failing to distinguish
each hypothesis. Preserve dead ends when they materially narrow the search.
Revise the relevance map and select the next diagnostic only if uncertainty
remains decision-relevant.

### 6. Establish Or Bound The Cause

When one explanation has a supported mechanism and alternatives are reasonably
excluded, state the causal chain and confidence. Otherwise, state the narrowest
remaining uncertainty and why current evidence cannot resolve it.

**Cause gate:** correlation, temporal adjacency, or a matching error string is
not sufficient without a mechanism connecting it to the symptom.

### 7. Recommend The Next Action

If the cause is supported and a repair is requested, hand off to `bug-fix`.
Otherwise recommend the smallest action that resolves the diagnosed condition
or collects the missing evidence. Keep diagnosis separate from speculative
repair.

### 8. Explain The Investigation

Communicate the path as:

```text
symptom -> baseline -> hypotheses -> distinguishing evidence -> causal conclusion or gap
```

Include only diagnostic branches that affected the conclusion or confidence.

## Allowed Iteration

- Iterate one distinguishing diagnostic at a time.
- Revisit a node only when new evidence creates a new question.
- Expand system scope only when all viable local hypotheses are contradicted or
  an observed edge crosses the current boundary.
- Stop low-value polling or retries that cannot change the hypothesis ranking.

## Stopping Conditions

Complete when:

- a causal explanation is supported and alternatives are bounded; or
- the unresolved gap is precise, externally constrained, and paired with the
  highest-value next diagnostic.

Stop as blocked when evidence cannot be observed safely or required access is
unavailable after meaningful alternatives have been exhausted.

## Output Contract

The final response must make recoverable:

- the precise symptom and baseline;
- the system location and relevant diagnostic path;
- hypotheses considered and evidence that changed their status;
- the supported cause and confidence, or the exact unresolved gap;
- diagnostics performed and observed results;
- the next action and why it has highest value.

Do not imply that diagnosis, mitigation, and permanent repair are the same
outcome.

## Quality Gate

Before finishing, confirm:

1. the symptom is observable and bounded;
2. competing hypotheses were considered;
3. each diagnostic had a defined distinguishing purpose;
4. causal language is supported by a mechanism;
5. dead ends and contradictory evidence are retained when material;
6. confidence matches evidence;
7. the human can explain what is known, what was ruled out, and what remains.
