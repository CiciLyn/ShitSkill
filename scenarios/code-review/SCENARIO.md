# Code Review Scenario

## Trigger

Use this scenario when the human asks to review a diff, change set, branch,
commit, pull request, or bounded implementation for defects and risk.

Route to `repo-understanding` when no bounded change exists and the goal is
general exploration. Route to `bug-fix` when the human asks to implement fixes
rather than review.

## Goal

Identify actionable, evidence-backed defects, regressions, security or
reliability risks, and material test gaps introduced by the reviewed change.

## Imports

Read and apply these modules in workflow order:

1. [`better-understanding`](../../modules/better-understanding/MODULE.md)
2. [`path-navigation`](../../modules/path-navigation/MODULE.md)
3. [`causal-reasoning`](../../modules/causal-reasoning/MODULE.md)
4. [`better-explanation`](../../modules/better-explanation/MODULE.md)

Use [`verification`](../../modules/verification/MODULE.md) when focused checks
can validate or falsify a candidate finding.

Apply these rules:

- [Context rules](../../rules/context-rules.md): Assume Minimal Human Context,
  Assume No Prerequisite Knowledge, Respect Limited Patience, Establish Context
  First, Progressive Disclosure.
- [Navigation rules](../../rules/navigation-rules.md): Explain Non-Obvious
  Transitions, Explain Why It Matters, Stay Goal-Relevant.
- [Explanation rules](../../rules/explanation-rules.md): Introduce Terms In
  Plain Language, Expand Compressed Language, Use Sentence-Level Analogies,
  Visualize Non-Trivial Relationships, Make Quantitative Reasoning
  Executable, Prefer Causal Relationships, Preserve Causal Order,
  Distinguish Fact From Inference, Cite Original Evidence, Verify Before
  Claiming Success.

## Inputs

- The exact review scope and changed lines.
- Stated intent, requirements, and compatibility expectations.
- Surrounding contracts, callers, tests, and runtime assumptions.
- Repository conventions and relevant user changes outside the diff.
- Available focused validation tools.

## Understanding Model

Use `Responsibility` and `Boundary` to identify the changed contract and its
owner. Add `Flow / sequence` or `State` when behavior crosses callers,
consumers, or lifecycle transitions. Use `Causality` to prove each retained
finding's trigger and impact.

## Workflow

### 1. Bound The Review

Identify the exact change set, its intended behavior, and the baseline against
which it should be judged. Separate changed code from pre-existing conditions.

**Scope gate:** do not attribute an issue to the change unless the change
introduces it, exposes it in a materially new way, or makes it relevant to the
requested review.

### 2. Build A Change Map

For each changed responsibility, identify:

- the contract or invariant affected;
- callers and downstream consumers;
- state, data, permission, or lifecycle transitions;
- tests intended to cover it.

Follow non-obvious edges outside the diff only when they are needed to assess
impact.

### 3. Derive Expected Behavior

Establish expected behavior from requirements, executable contracts, existing
tests, stable conventions, or directly related implementation. Label ambiguity
instead of inventing a requirement.

### 4. Generate Candidate Findings

Inspect how the change behaves under:

- normal and boundary inputs;
- error, cancellation, and partial-failure paths;
- state and lifecycle transitions;
- concurrency or ordering assumptions;
- compatibility and migration;
- security and permission boundaries;
- testability and observability.

A stylistic preference is not a finding unless it creates a concrete
maintainability or correctness risk.

### 5. Prove Or Reject Each Finding

For each candidate, establish:

```text
changed condition -> triggering situation -> incorrect behavior -> user or system impact
```

Use direct code evidence and focused checks when useful. Reject candidates that
depend on implausible conditions, unsupported requirements, or behavior already
prevented elsewhere.

**Finding gate:** report only when the issue is specific, actionable, tied to
the reviewed change, and supported by a reproducible path or defensible
mechanism.

### 6. Assign Priority

Rank findings by practical impact and likelihood, not code complexity. A
finding's priority must be explainable from its trigger and consequence.

Group duplicate symptoms under one root finding.

### 7. Assess Coverage

Identify missing tests only when they leave a material behavior, regression, or
contract unprotected. Distinguish:

- a defect proven by current evidence;
- a plausible risk requiring validation;
- a coverage gap without a proven defect.

### 8. Report Findings First

Present findings in descending severity. Each finding must include:

- concise title and priority;
- precise file and line range;
- triggering condition;
- causal explanation and impact;
- practical correction direction.

After findings, include open questions or assumptions, then a brief change
summary. If no findings survive the finding gate, say so clearly and state
remaining test gaps or residual risk.

## Allowed Iteration

- A candidate finding may trigger a focused path trace or verification check.
- Contradictory evidence removes or narrows the finding.
- Scope may expand outside changed files only along a named contract,
  caller, consumer, or runtime edge.
- Do not turn review into implementation unless the human asks for fixes.

## Stopping Conditions

Complete when:

- every material changed responsibility has been assessed;
- all reported findings pass the finding gate;
- duplicate or unsupported candidates are removed;
- coverage gaps and assumptions are explicit.

Stop as blocked when the diff, baseline, generated source, or required contract
is unavailable and the missing evidence prevents responsible findings.

## Output Contract

The final response must contain, in order:

1. findings ordered by severity with precise code references;
2. open questions or assumptions that materially affect confidence;
3. a brief change summary;
4. test gaps or residual risk.

If there are no findings, state that explicitly before the remaining risks. Do
not bury findings under a general summary.

## Quality Gate

Before finishing, confirm:

1. every finding is caused or exposed by the reviewed change;
2. every finding includes a realistic trigger and concrete impact;
3. evidence supports the claimed causal path;
4. priorities reflect user or system consequences;
5. code references are narrow enough to act on;
6. uncertainty and coverage gaps are not presented as proven defects;
7. the response leads with findings rather than praise or summary.
