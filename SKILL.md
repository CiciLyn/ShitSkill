---
name: "shit-skill"
description: "Builds evidence-backed mental models. Invoke when users ask to understand or explain why/how code, a codebase, architecture, documents, failures, debugging evidence, or causal relationships work."
---

# Shit Skill

Use this skill to help a human complete a technical task without losing the
context, transitions, evidence, and causal relationships that make the result
understandable.

The skill communicates decision-relevant rationale and evidence. It does not
expose hidden chain-of-thought.

## Architecture

- `rules/` contains atomic constraints that must remain true.
- `modules/` contains reusable methods for satisfying those constraints.
- `scenarios/` defines how a concrete task composes modules and rules.

Keep these boundaries strict:

- A rule is one sentence and does not prescribe a workflow.
- A module is reusable and does not select rules, direct other modules, or
  branch on scenario names.
- A scenario references modules and rules without copying them.
- Workflow, module ordering, handoffs, and iteration belong to the scenario.

## Start Every Task

1. Read [`rules/README.md`](rules/README.md).
2. Classify the request using [`scenarios/README.md`](scenarios/README.md).
3. Read the selected scenario's `SCENARIO.md` completely.
4. Read the grouped rule documents and modules imported by that scenario.
5. Execute the scenario's workflow, gates, iteration rules, stopping
   conditions, and output contract.
6. If the requested outcome changes, select the new scenario explicitly and
   satisfy its completion conditions.

## Scenario Execution

Treat the selected scenario as the runner:

```text
scenario
  -> imports rules and modules
  -> supplies task-specific inputs
  -> selects the required mental-model primitives
  -> orders the workflow
  -> enforces decision gates
  -> controls evidence-driven iteration
  -> applies stopping conditions
  -> checks the output contract
```

Do not copy module procedures into the scenario or turn output contracts into
fixed prose templates. The scenario controls behavior; the visible response
structure should match the task's complexity and the human's demonstrated
context.

## Completion Test

Before finishing, check that the human can recover:

- what was examined or changed;
- where it sits in the larger system;
- why the relevant path was followed;
- how the important parts connect;
- how concrete runtime behavior travels through lookup, dispatch, wrappers, and
  execution boundaries to its observable effect;
- what specialized terms do, what capability they control, and why they matter
  in the current path;
- what each quantitative symbol and unit means, why the stated relationship
  holds, and whether each condition is derived, evidence-backed, or assumed;
- what evidence supports the conclusion;
- which claims are proven by implementation, configuration, runtime evidence,
  documentation, or labeled inference;
- what remains unknown or outside scope;
- what was verified and with what result.

If these cannot be recovered, the task is not yet communicated completely.
