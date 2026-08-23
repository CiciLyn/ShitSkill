# Better Explanation

## Purpose

Turn an established mental model into an explanation that a lower-context human
can follow, verify, and reuse.

This module determines **how to communicate what is already understood**. It
does not establish truth, choose the task workflow, or replace missing evidence.

## Inputs

- A goal-relevant mental model.
- The human's demonstrated context and requested depth.
- Facts, inferences, unknowns, and supporting evidence.
- Important relationships and transitions.
- The outcome or decision the explanation must support.

If the mental model is incomplete, report the missing input instead of hiding
the gap with polished prose.

## Method

### 1. Set The Entry Point

Begin with the smallest orientation that makes the remaining explanation
meaningful:

- the question or outcome;
- the system location;
- the central conclusion, when already supported.

Do not begin with a deep implementation detail or unexplained terminology.

### 2. Choose A Conceptual Spine

Arrange the explanation around one connected path. Common spines include:

```text
What -> Why -> How -> Impact
```

```text
Problem -> Context -> Cause -> Decision -> Action -> Result
```

The scenario chooses the appropriate spine. Do not combine several competing
structures unless the task genuinely has independent subproblems.

### 3. Reveal Detail In Layers

Move through these information layers only as needed:

1. conclusion or orientation;
2. relevant map;
3. relationships and causal chain;
4. local implementation or evidence;
5. impact, verification, and unknowns.

Each layer must make the next layer easier to understand. Stop descending when
additional detail no longer changes the human's decision or mental model.

### 4. Expand Compressed Meaning

When an unfamiliar term first matters, explain it in this order:

```text
term -> plain-language role -> precise meaning -> relevance here
```

Do not replace one unfamiliar term with several others. Reuse the precise term
after its meaning has been established.

### 5. Explain Relationships, Not Just Objects

For every non-obvious move from one item to another, state:

- what connects them;
- why the explanation moves there;
- what the destination contributes to the goal.

Prefer verbs such as calls, produces, validates, stores, constrains, or depends
on over unlabeled arrows.

### 6. Control Cognitive Load

Group related details under one claim, keep evidence adjacent to that claim,
and omit irrelevant branches. When an omitted branch is an obvious alternative,
state briefly why it does not matter.

Use examples only when they resolve an abstraction or demonstrate a
relationship; examples must not become a second unexplained system.

### 7. Close The Loop

End by reconnecting local details to the original goal. State:

- the supported conclusion or completed action;
- its impact;
- the evidence or verification status;
- material unknowns or excluded scope.

## Explanation Plan

Before producing a substantial explanation, build this compact internal
artifact:

```text
Human context:
Goal:
Entry point:
Conceptual spine:
Key relationships:
Terms to expand:
Evidence placement:
Details to omit:
Closing loop:
```

This is a planning contract, not a mandatory user-facing template.

## Non-Goals

This module does not:

- infer facts that evidence does not support;
- decide which system areas are relevant;
- prescribe scenario-specific section headings;
- maximize detail for its own sake;
- expose hidden chain-of-thought.

## Quality Gate

The module is complete when:

1. the entry point establishes enough context for the first detail;
2. every important transition has an explicit relationship and reason;
3. unfamiliar terms are understandable at first meaningful use;
4. details appear in a coherent progression rather than as disconnected facts;
5. the conclusion reconnects evidence and impact to the original goal;
6. facts, inferences, unknowns, and verification status remain distinguishable.
