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

### 4. Draw When Relationships Are Non-Trivial

| Representation | Use for |
| --- | --- |
| ASCII / Markdown | A short linear path or small hierarchy. |
| Mermaid `flowchart` | Components, dependencies, control flow, or branches. |
| Mermaid `sequenceDiagram` | Time-ordered interactions between actors. |
| Mermaid `stateDiagram-v2` | Lifecycle and state transitions. |

A useful diagram:

- contains only goal-relevant nodes;
- labels edges with meaningful verbs;
- makes the target and boundary visible;
- distinguishes uncertain relationships;
- includes one sentence stating its main takeaway.

Do not draw a diagram when prose is clearer.

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
Diagram, when useful:
Prediction:
Evidence gaps:
```

Populate only relevant fields.

## Boundaries

Do not select the model, inspect the whole system, prove causal claims,
prescribe a scenario workflow, require a diagram, or dictate the final
explanation format.

## Quality Gate

The human can locate the target, explain the relevant responsibilities and
relationships, trace the important behavior, and predict the next outcome.
