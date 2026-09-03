# Scenario Catalog

Scenarios answer one question: **how should modules and rules be composed for
this task?**

A scenario is an executable specification, not a response template. It owns the
task goal, module ordering, selected rules, scenario-specific inputs, decision
gates, stopping conditions, and output contract. It must reference shared
modules and rules rather than copy their instructions.

## Scenarios

| Scenario | Goal | Status |
| --- | --- | --- |
| [`bug-fix`](bug-fix/SCENARIO.md) | Find and fix the root cause of an observed defect. | Implemented |
| [`code-review`](code-review/SCENARIO.md) | Identify evidence-backed defects, regressions, risks, and test gaps. | Implemented |
| [`repo-understanding`](repo-understanding/SCENARIO.md) | Build a useful mental model of a repository around the human's goal. | Implemented |
| [`module-development`](module-development/SCENARIO.md) | Design, implement, and verify a bounded capability within an existing system. | Implemented |
| [`debugging`](debugging/SCENARIO.md) | Reduce an uncertain failure to a supported cause or explicit evidence gap. | Implemented |
| [`document-understanding`](document-understanding/SCENARIO.md) | Explain a document's problem, concepts, relationships, flow, and conclusions. | Implemented |
| [`architecture-understanding`](architecture-understanding/SCENARIO.md) | Explain system boundaries, responsibilities, interactions, and tradeoffs. | Implemented |

`code-understanding` routes to `repo-understanding` or `module-development`
according to scope. `report` remains an output concern rather than a standalone
scenario.

## Routing

Choose the scenario by the requested outcome:

- Unknown failure cause -> `debugging`.
- Supported defect that must be repaired -> `bug-fix`.
- New bounded capability -> `module-development`.
- Assessment of a bounded change -> `code-review`.
- Navigation and mental model for a repository -> `repo-understanding`.
- Faithful understanding of a source document -> `document-understanding`.
- System boundaries, interactions, invariants, or tradeoffs ->
  `architecture-understanding`.

When a task changes outcome, hand off explicitly. For example, debugging may
discover a supported cause and then hand off to bug fixing. Do not silently
blend completion conditions from two scenarios.

## Scenario Contract

Each implemented scenario must define:

1. **Trigger**: requests that activate the scenario and requests that do not.
2. **Goal**: the outcome the workflow must achieve.
3. **Imports**: required modules and rules by relative path.
4. **Inputs**: task-specific evidence and constraints.
5. **Understanding model**: mental-model primitives selected for this task.
6. **Workflow**: ordered phases, decision gates, and allowed iteration.
7. **Stopping conditions**: completion and blocked states.
8. **Output contract**: required evidence and conclusions, not fixed prose.
9. **Quality gate**: checks proving that the workflow and human mental model are complete.

Every scenario must select `Cite Original Evidence`.

Any scenario that permits code, configuration, data, or external-state changes
must select `Explain Change Before Action`.

Every scenario must select the complete reader model: `Assume Minimal Human
Context`, `Assume No Prerequisite Knowledge`, `Respect Limited Patience`,
`Establish Context First`, and `Progressive Disclosure`.

Every scenario must also select `Introduce Terms In Plain Language`, `Expand
Compressed Language`, `Use Sentence-Level Analogies`, and `Visualize
Non-Trivial Relationships`; a scenario may omit an analogy or visual only when
the corresponding rule's applicability condition is not met.

## Status

All first-version scenario workflows are implemented. New scenarios must
compose the existing modules and rules unless a genuinely reusable method or
global invariant is missing.
