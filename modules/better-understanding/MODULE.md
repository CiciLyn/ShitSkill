# Better Understanding

## Purpose

Build the smallest mental model that makes the target **mentally executable**:
the human can locate it, trace the relevant behavior, and predict what happens
next.

This module decides what must be understood, not the scenario workflow or final
response format.

## Mental Model Primitives

A scenario selects the model primitives required by its task. This module
defines how to build the selected model.

| Model | Question |
| --- | --- |
| Structure | What exists and how is it organized? |
| Flow / sequence | How do control or data move, and in what order? |
| State | What states exist and what causes transitions? |
| Responsibility | Who owns each decision, operation, or invariant? |
| Causality | Why does one condition produce another? |
| Boundary | What matters, and what is outside scope? |

## Build The Model

### 1. Accept The Target And Model

Use the goal, target, boundary, and model primitives supplied by the scenario.
Define what the human should be able to trace or predict when understanding is
sufficient.

### 2. Keep Only Relevant Parts

For each selected part, capture:

- its plain-language responsibility;
- why it matters to the target;
- its relationship to another selected part.

Include neighbors only when they establish a boundary or necessary dependency.

### 3. Connect Parts With Labeled Edges

A component list is not a mental model. Show what moves or changes:

```text
request
  -> enters through
controller
  -> delegates validation to
service
  -> writes
store
```

Use only the dimensions that matter: control, data, state, responsibility, or
causality.

### 4. Externalize Non-Trivial Relationships

Default to a visual model when the human would otherwise need to hold several
relationships in working memory. Draw when the target includes any of these:

- more than two components with different responsibilities;
- a branch, fallback, retry, or causal fork;
- interactions whose order changes the result;
- lifecycle states or transitions;
- boundaries that determine who can read, write, call, or clean up.

| Representation | Use for |
| --- | --- |
| ASCII | Short paths when rendering is uncertain. |
| Mermaid `flowchart` | Components, control flow, causes, or branches. |
| Mermaid `sequenceDiagram` | Ordered calls, messages, and returns. |
| Mermaid `stateDiagram-v2` | States and transition triggers. |
| Table | Comparisons without position or time. |

A useful diagram:

- contains only goal-relevant nodes;
- labels edges with plain-language actions rather than compressed nouns;
- makes the target and boundary visible;
- distinguishes uncertain relationships;
- remains readable without zooming into implementation trivia;
- includes one sentence stating its main takeaway.

Introduce the question that the visual answers, render the visual, then state
the conclusion the human should take from it. The visual reduces mental
assembly; it does not replace definitions, evidence, or causal explanation.

Omit a diagram only when the relationship is genuinely simpler as prose. When
Mermaid rendering is unavailable, preserve the same relationships with ASCII
instead of dropping the visual model.

### 5. Apply The Predictive Check

Ask:

> Can the human trace the path and predict what happens next when the important
> step succeeds or fails?

If not, the model is incomplete or at the wrong abstraction level.

## Output

```text
Goal and target:
Scenario-selected model:
Relevant parts and responsibilities:
Labeled relationships:
Boundary:
Visual model, or reason omitted:
Prediction:
Evidence gaps:
```

Populate only relevant fields.

## Boundaries

Do not select the model, inspect the whole system, prove causal claims,
prescribe a scenario workflow, force a diagram when no visual trigger exists,
or dictate the final explanation format.

## Quality Gate

The human can locate the target, explain the relevant responsibilities and
relationships, trace the important behavior, and predict the next outcome;
non-trivial relationships are externalized in a labeled visual model or have a
specific reason why prose is clearer.
