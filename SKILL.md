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
  attempt that merely repeats the first explanation;
- attention already divided among other tasks, messages, and decisions, so the
  explanation must continually earn its place.

These are communication constraints, not judgments about the human. Never
mention this model to the human, patronize them, or reduce technical precision.
Instead, supply the missing context, connect every required intermediate step,
lead with the conclusion or next action that matters, and make the
explanation easy to scan. Earn attention with relevance and visible progress,
not suspense, clickbait, or decorative novelty.

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
5. When resuming a complex explanation, recover the previous checkpoint's
   node IDs, statuses, follow-up questions, and remaining queue before adding
   or selecting nodes.
6. Execute the scenario's workflow, gates, iteration rules, stopping
   conditions, and output contract.
7. If the requested outcome changes, select the new scenario explicitly and
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
- which names are exact source identifiers, canonical source terms,
  plain-language relationships, or explicitly introduced explanatory
  shorthand;
- how a concrete value is renamed across constructor arguments, instance
  attributes, function parameters, or other source scopes;
- how each analogy maps a relationship in the real system, and where that
  analogy stops being accurate;
- what question each substantial section answers, why it matters at that point,
  and what understanding or decision it gives the human;
- why any mathematical notation was necessary, what each term, symbol, and unit
  means in plain language, where the relationship comes from, and why its
  premises apply to the current case;
- what evidence supports the conclusion;
- which complete shallow node map orients a complex explanation before local
  detail begins;
- which no-more-than-three nodes were selected for deep explanation in the
  current turn, unless the human explicitly requested one exhaustive pass;
- which nodes were explained, which follow-up questions remain, and which
  queued nodes should continue in a later turn;
- which claims are proven by implementation, configuration, runtime evidence,
  documentation, or labeled inference;
- what remains unknown or outside scope;
- what was verified and with what result.

If these cannot be recovered, the task is not yet communicated completely.
