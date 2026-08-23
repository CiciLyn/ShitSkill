# Path Navigation

## Purpose

Trace a goal-relevant path across artifacts, components, concepts, and
abstraction levels while making every non-obvious transition explainable.

This module determines **where to go next and why**. It does not prove that a
traced relationship is causal or decide the scenario's overall workflow.

## Inputs

- The current goal and system location.
- A starting node supported by the observed task or evidence.
- A goal-relevant map of candidate nodes and boundaries.
- Available structural evidence such as calls, imports, references, data flow,
  ownership, configuration, logs, or documentation links.
- Scope and stopping conditions.

## Method

### 1. Anchor The Path

Name the starting node and explain why the task makes it the correct entry
point. A node may be a file, function, service, event, configuration value,
document section, log record, or concept.

Do not choose an entry point only because it looks technically important.

### 2. State The Navigation Question

Before leaving a node, state what the next transition must discover, such as:

- Who calls this?
- Where does this value come from?
- Which component changes this state?
- Where is this behavior configured?
- Which evidence supports this claim?

The question constrains the search and makes the next node meaningful.

### 3. Follow A Supported Edge

Choose the next node using an observable edge. Label the edge with its actual
relationship:

```text
calls
returns
reads
writes
emits
handles
configures
owns
documents
contradicts
```

Record whether the edge is directly observed or inferred. An inferred edge must
include its supporting facts and remain provisional.

### 4. Explain The Transition

For every non-obvious transition, record:

```text
From:
To:
Relationship:
Why this transition:
Evidence:
Question answered:
```

Do not merely explain what the destination does. Explain why reaching it
advances the current goal.

### 5. Control Branching

When several outgoing edges are available:

1. rank them by relevance to the navigation question;
2. follow the smallest set that can answer it;
3. note obvious alternatives that were excluded;
4. explain why an excluded branch is currently lower value.

Explore a second branch only when the first branch is disproved, incomplete, or
insufficient to distinguish competing explanations.

### 6. Handle Dead Ends And Loops

If a path stops producing evidence, mark the dead end and return to the last
supported branch point. If the path revisits a node, state what new question or
evidence justifies the revisit.

Do not silently jump to an unrelated path.

### 7. Stop At A Decision-Relevant Node

Stop navigation when the path has located enough evidence to support the
scenario's next decision, or when remaining routes cannot be distinguished with
available evidence.

Report an evidence gap instead of extending the path by speculation.

## Path Ledger

Maintain this compact internal artifact:

```text
Goal:
Entry point:
Navigation question:
Path:
  node A --relationship/evidence--> node B
  node B --relationship/evidence--> node C
Excluded branches:
Dead ends:
Current answer:
Remaining gap:
Stop reason:
```

This ledger is not a mandatory user-facing format.

## Non-Goals

This module does not:

- traverse every reference or dependency;
- treat proximity, ordering, or correlation as causation;
- hide failed paths that materially affect confidence;
- replace scenario-specific search or debugging procedures;
- expose hidden chain-of-thought.

## Quality Gate

The module is complete when:

1. the entry point is tied to the goal;
2. every retained transition has a named relationship and evidence;
3. the reason for choosing each next node is explicit;
4. excluded branches and dead ends are accounted for when material;
5. the path stops for a stated decision-relevant reason;
6. facts and inferred links remain distinguishable.
