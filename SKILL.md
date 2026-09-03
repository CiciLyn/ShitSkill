---
name: "shit-skill"
description: "Builds evidence-backed mental models for low-context, impatient readers. Invoke to explain code, architecture, documents, failures, debugging evidence, or causal relationships."
---

# Shit Skill

Use this skill to help a human complete a technical task without losing the
context, transitions, evidence, and causal relationships that make the result
understandable.

The skill communicates decision-relevant rationale and evidence. It does not
expose hidden chain-of-thought.

## Reader Model

Design every explanation for a human who may have:

- little context about the current task or system;
- little familiarity with the relevant domain;
- little patience for unexplained detours, delayed conclusions, or a second
  attempt that merely repeats the first explanation.

These are communication constraints, not judgments about the human. Never
mention this model to the human, patronize them, or reduce technical precision.
Instead, supply the missing context, connect every required intermediate step,
lead with the conclusion or next action that matters, and make the
explanation easy to scan.

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
- which visual model shows a non-trivial structure, flow, sequence, or state
  change, and what conclusion the human should read from it;
- how one representative trigger moves concrete values through those parts,
  including what is temporary, persistent, and cleaned up;
- how concrete runtime behavior travels through lookup, dispatch, wrappers, and
  execution boundaries to its observable effect;
- what specialized terms do, what capability they control, and why they matter
  in the current path;
- how compressed phrases were expanded into complete statements that name who acts,
  what they do, and what changes;
- how each analogy maps a relationship in the real system, and where that
  analogy stops being accurate;
- why any mathematical notation was necessary, what each term, symbol, and unit
  means in plain language, where the relationship comes from, and why its
  premises apply to the current case;
- what evidence supports the conclusion;
- which claims are proven by implementation, configuration, runtime evidence,
  documentation, or labeled inference;
- what remains unknown or outside scope;
- what was verified and with what result.

If these cannot be recovered, the task is not yet communicated completely.
