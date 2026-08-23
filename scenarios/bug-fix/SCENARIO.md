# Bug Fix Scenario

## Trigger

Use this scenario when the human reports incorrect behavior and asks to correct
the implementation.

Route elsewhere when:

- the cause is still broadly uncertain and the immediate goal is diagnosis:
  use `debugging`;
- the request adds a capability rather than restores expected behavior: use
  `module-development`;
- the request asks only for critique without changes: use `code-review`.

## Goal

Identify the defect's supported root cause, correct it at the responsible
boundary, and verify that expected behavior is restored without unacceptable
regression.

## Imports

Read and apply these modules in workflow order:

1. [`better-understanding`](../../modules/better-understanding/MODULE.md)
2. [`path-navigation`](../../modules/path-navigation/MODULE.md)
3. [`causal-reasoning`](../../modules/causal-reasoning/MODULE.md)
4. [`verification`](../../modules/verification/MODULE.md)
5. [`better-explanation`](../../modules/better-explanation/MODULE.md)

Apply these rules:

- [Context rules](../../rules/context-rules.md): Assume Limited Human Context,
  Establish Context First, Progressive Disclosure.
- [Navigation rules](../../rules/navigation-rules.md): Explain Non-Obvious
  Transitions, Explain Why It Matters, Stay Goal-Relevant.
- [Explanation rules](../../rules/explanation-rules.md): Prefer Causal
  Relationships, Preserve Causal Order, Distinguish Fact From Inference,
  Cite Original Evidence, Explain Change Before Action, Verify Before Claiming
  Success.

## Inputs

- Observed behavior, expected behavior, and reproduction context.
- Relevant repository state, constraints, and existing user changes.
- Error output, logs, failing checks, or other direct evidence.
- The affected interface, workflow, or invariant.
- Available verification tools and risk boundaries.

## Understanding Model

Use `Causality` as the primary model. Add `Flow / sequence` to trace the failing
path, `State` when a transition is violated, and `Responsibility` plus
`Boundary` to locate the correct repair owner. Use `Structure` only for the
minimum orientation needed to follow that path.

## Workflow

### 1. Establish The Defect

Translate the report into an observable difference between expected and actual
behavior. Locate the user-visible or system-visible entry point and define what
would count as restored behavior.

**Symptom gate:** do not edit while the defect cannot be stated as an
observable mismatch. If evidence is insufficient, gather a focused observation
or route to `debugging`.

### 2. Trace The Relevant Execution Path

Start from the observed entry point and follow only supported control, data,
state, or configuration edges. Explain why each file, component, or function is
the next relevant node. Record material dead ends and excluded branches.

### 3. Establish Root Cause

Connect the violated expectation to the mechanism that produces the symptom.
Distinguish the faulty condition from the place where the symptom merely
surfaces. Challenge the explanation against plausible alternatives.

**Cause gate:** implementation may change only after evidence supports a causal
chain and identifies the violated responsibility or invariant. A plausible
location is not enough.

### 4. Choose The Repair Boundary

Select the narrowest responsible boundary that restores the invariant. Compare
obvious alternatives and explain why they would mask the symptom, duplicate
responsibility, or expand risk.

**Repair gate:** the proposed change must state its expected before/after
behavior, affected boundary, and predicted impact before editing.

### 5. Implement The Repair

Make the smallest coherent change consistent with repository conventions.
Preserve unrelated user changes and avoid unrelated refactors. Add or adjust
focused coverage when the defect can recur undetected.

If implementation evidence invalidates the causal account, stop editing and
return to path tracing rather than extending a speculative patch.

### 6. Verify The Outcome

Verify the original failure path first, then the restored invariant and
material neighboring behavior. Scale checks to the blast radius. Classify each
important claim as passed, failed, inconclusive, or not run.

**Completion gate:** a successful command is insufficient unless its
observation supports the repaired behavior.

### 7. Explain The Completed Path

Communicate the result in causal order:

```text
symptom -> relevant path -> root cause -> repair boundary -> change -> verification
```

Keep evidence adjacent to the claim it supports and reconnect local changes to
the observed defect.

## Allowed Iteration

- Verification failure returns to root-cause analysis when it contradicts the
  causal account.
- Verification failure returns to implementation when the cause remains
  supported but the repair is incomplete.
- New evidence may expand scope only with an explicit reason tied to the
  original defect.
- Do not replay external side effects merely to gain confidence unless the
  scenario's domain workflow makes the repetition safe.

## Stopping Conditions

Complete when:

- the root cause is supported by evidence;
- the repair is applied at the responsible boundary;
- the original behavior and material impact are verified;
- residual risk and unrun checks are explicit.

Stop as blocked when required evidence, access, reproduction, or safe
verification is unavailable and no meaningful local progress remains. Report
the exact gap and the next observation needed.

## Output Contract

The final response must make recoverable:

- the defect and its system location;
- the relevant path and reason for each non-obvious transition;
- the supported root cause;
- why this repair boundary was chosen;
- the concrete change and intended impact;
- checks run, observed results, and coverage;
- residual risk, unknowns, or checks not run.

This is a content contract, not a mandatory heading template.

## Quality Gate

Before finishing, confirm:

1. observed and expected behavior are distinct and evidenced;
2. the symptom location is not confused with the cause;
3. each retained path transition has a reason;
4. the repair restores an explicit invariant at the correct boundary;
5. unrelated changes were not introduced;
6. verification supports the success language;
7. the human can restate why the defect occurred and why the change fixes it.
