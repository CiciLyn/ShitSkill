# Top-Down

## Purpose

Descend from the highest abstraction relevant to the human's goal into the
minimum necessary implementation detail without losing orientation.

This module defines **how to control depth across abstraction levels**. A
scenario defines what those levels mean for its domain.

## Inputs

- The current goal and completion condition.
- A goal-relevant map of the target and its surroundings.
- The available hierarchy, graph, or conceptual structure.
- The human's demonstrated context and requested depth.
- Candidate branches and their relevance to the goal.

## Method

### 1. Choose The Top Anchor

Start at the highest level that is both relevant and necessary. The top anchor
must answer:

- What larger system or concept contains the target?
- What role does the target play there?
- Why is this level useful for the current goal?

Do not start at the highest imaginable level when it adds no decision-relevant
context.

### 2. Define Scenario Levels

Ask the scenario to map its domain into ordered levels. The generic shape is:

```text
purpose
  -> major structure
  -> relevant responsibility
  -> interaction path
  -> local mechanism
  -> implementation detail
```

The module supplies the descent method, not fixed domain labels.

### 3. Select Relevant Branches

At each level:

1. list only the few branches needed to orient the human;
2. identify which branch advances the goal;
3. explain why that branch deserves deeper inspection;
4. bound obvious alternatives that will not be explored.

Do not give every sibling equal depth.

### 4. Descend One Meaningful Level At A Time

Before moving down, state:

- the current level;
- the next level;
- the relationship between them;
- the question the deeper level will answer.

Do not jump directly from a system overview to a line-level detail unless the
intermediate relationship is already established.

### 5. Apply A Depth Gate

After each descent, ask:

- Has the current goal been answered?
- Would another level change the conclusion, action, or confidence?
- Does the human need this detail to reconstruct the mental model?

Stop when all answers indicate that deeper detail is unnecessary.

### 6. Re-Anchor After Local Detail

After examining local mechanisms, reconnect them to:

- the parent responsibility;
- the relevant path;
- the original goal;
- the resulting conclusion or action.

This prevents the explanation from ending at an isolated implementation detail.

## Descent Plan

Create this compact internal artifact:

```text
Goal:
Top anchor:
Scenario-defined levels:
Selected branch at each level:
Reason for each descent:
Excluded branches:
Depth stop condition:
Return-to-goal statement:
```

This is a control structure, not a mandatory output outline.

## Non-Goals

This module does not:

- require every task to begin with a repository-wide overview;
- explore every branch in a hierarchy;
- define domain-specific levels;
- replace causal tracing across non-hierarchical relationships;
- force a fixed number of levels.

## Quality Gate

The module is complete when:

1. the top anchor is relevant to the goal;
2. each descent has an explicit purpose;
3. selected branches receive more depth than irrelevant siblings;
4. no required abstraction level is silently skipped;
5. the stopping depth is justified;
6. local detail is reconnected to the original goal.
