# Module Development Scenario

## Trigger

Use this scenario when the human asks to add or materially extend a bounded
capability inside an existing system.

Route to `bug-fix` when the requested behavior already exists by contract but is
broken. Route to `repo-understanding` when the immediate goal is exploration
rather than implementation.

## Goal

Define the capability and its boundary, integrate it with existing contracts
and conventions, implement it coherently, and verify the expected behavior and
impact.

## Imports

Read and apply these modules in workflow order:

1. [`better-understanding`](../../modules/better-understanding/MODULE.md)
2. [`top-down`](../../modules/top-down/MODULE.md)
3. [`causal-reasoning`](../../modules/causal-reasoning/MODULE.md)
4. [`verification`](../../modules/verification/MODULE.md)
5. [`better-explanation`](../../modules/better-explanation/MODULE.md)

Use [`path-navigation`](../../modules/path-navigation/MODULE.md) when integration
crosses non-obvious files, services, contracts, or runtime paths.

Apply these rules:

- [Context rules](../../rules/context-rules.md): Assume Minimal Human Context,
  Assume No Prerequisite Knowledge, Respect Limited Patience, Establish Context
  First, Progressive Disclosure.
- [Navigation rules](../../rules/navigation-rules.md): Explain Non-Obvious
  Transitions, Explain Why It Matters, Stay Goal-Relevant, Maintain Zoom
  Coherence.
- [Explanation rules](../../rules/explanation-rules.md): Introduce Terms In
  Plain Language, Expand Compressed Language, Use Sentence-Level Analogies,
  Visualize Non-Trivial Relationships, Make Quantitative Reasoning
  Executable, Prefer Causal Relationships, Distinguish Fact From
  Inference, Cite Original Evidence, Explain Change Before Action, Verify
  Before Claiming Success.

## Inputs

- Requested behavior, users, and completion criteria.
- Existing system boundaries, contracts, conventions, and ownership.
- Relevant interfaces, data shapes, state transitions, and failure behavior.
- Compatibility, migration, performance, security, and operational constraints.
- Existing tests and available verification environment.

## Understanding Model

Use `Responsibility` and `Boundary` to place the capability at the correct
extension point. Add `Structure` for integration context, `Flow / sequence` and
`State` for observable behavior, and `Causality` when comparing design
consequences.

## Workflow

### 1. Define The Capability

Translate the request into observable behavior, explicit non-goals, and
acceptance criteria. Identify who invokes the capability, what it consumes and
produces, and how failure should appear.

**Goal gate:** do not design or edit until the capability can be distinguished
from adjacent responsibilities.

### 2. Locate The Integration Boundary

Descend from system purpose to the existing module, contract, and extension
point relevant to the capability. Explain why this location owns the behavior
and why nearby alternatives do not.

Inspect repository conventions and analogous implementations before inventing
new structure.

### 3. Establish Contracts And Invariants

Define or confirm:

- public input and output contracts;
- state and lifecycle expectations;
- error and cancellation behavior;
- compatibility requirements;
- invariants that must remain true.

Separate requirements supported by the request or existing system from design
inferences.

**Contract gate:** implementation begins only when callers, ownership, and
observable behavior are sufficiently clear.

### 4. Choose The Design

Compare the smallest viable design with material alternatives. Prefer existing
patterns and helpers. Add an abstraction only when it removes meaningful
complexity, duplication, or contract ambiguity.

Predict how the design changes control, data, or state and identify affected
boundaries.

**Design gate:** the selected design must explain why it fits the current
architecture and how it satisfies each acceptance criterion.

### 5. Implement In Dependency Order

Implement foundational contracts and lower-level behavior before callers and
presentation layers. Keep edits within the selected ownership boundary and
preserve unrelated user changes.

After each coherent slice, check whether implementation evidence invalidates a
contract or design assumption. If so, return to the relevant gate.

### 6. Verify Behavior And Integration

Map each acceptance criterion and material invariant to a proportionate check.
Verify focused behavior first, then integration boundaries and important
negative cases. Include broader checks when shared contracts or user-visible
flows are affected.

### 7. Explain The Delivered Capability

Communicate:

```text
goal -> system boundary -> contracts -> design decision -> implementation -> verification -> impact
```

Explain new terms and non-obvious file transitions, but do not narrate every
edit.

## Allowed Iteration

- Discovery may return to capability definition when existing contracts
  contradict the request.
- Implementation may return to design when a local pattern exposes a simpler
  or safer integration.
- Failed verification returns to implementation or contract definition
  according to what the evidence contradicts.
- Scope expansion requires an explicit dependency on an acceptance criterion.

## Stopping Conditions

Complete when:

- acceptance criteria and non-goals are explicit;
- implementation is integrated at the responsible boundary;
- relevant contracts and invariants are preserved;
- checks support the claimed behavior and impact;
- residual gaps are stated.

Stop as blocked when a required product decision, unavailable dependency,
permission, or unsafe migration prevents a coherent implementation.

## Output Contract

The final response must make recoverable:

- the delivered capability and non-goals;
- where it fits in the system and why;
- contracts or invariants introduced or preserved;
- important design decisions and rejected alternatives;
- files or components changed and their responsibilities;
- verification evidence and observed results;
- compatibility impact, residual risk, and unresolved decisions.

This is a content contract, not a fixed implementation report template.

## Quality Gate

Before finishing, confirm:

1. the capability has observable acceptance criteria;
2. ownership and integration boundaries are explicit;
3. design follows existing patterns unless deviation is justified;
4. dependencies were implemented in coherent order;
5. every material acceptance criterion has evidence or a named gap;
6. impact and compatibility are bounded;
7. the human can explain what was added, where it lives, and why it is designed this way.
