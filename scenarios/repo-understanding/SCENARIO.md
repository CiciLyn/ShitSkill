# Repository Understanding Scenario

## Trigger

Use this scenario when the human wants to understand a repository, codebase, or
broad subsystem and needs a goal-relevant mental model before working in it.

Route to `module-development` when the request includes implementing a bounded
capability. Route to `debugging` or `bug-fix` when an observed failure is the
primary organizing goal.

## Goal

Explain what the repository does, how its important responsibilities are
organized, how the paths relevant to the human's goal execute, and where deeper
implementation work should begin.

## Imports

Read and apply these modules in workflow order:

1. [`better-understanding`](../../modules/better-understanding/MODULE.md)
2. [`top-down`](../../modules/top-down/MODULE.md)
3. [`path-navigation`](../../modules/path-navigation/MODULE.md)
4. [`better-explanation`](../../modules/better-explanation/MODULE.md)

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
  Executable, Prefer Causal Relationships, Distinguish Fact From Inference, Cite Original Evidence.

## Inputs

- The human's goal, expected task, and requested depth.
- Repository structure, entry points, manifests, documentation, and tests.
- Runtime, build, deployment, or data-flow artifacts relevant to the goal.
- Known ownership boundaries and generated or vendored areas.
- Current branch or version when behavior may vary over time.

## Understanding Model

Use `Structure` as the primary model, then add `Responsibility` and
`Flow / sequence` for the paths relevant to the human's goal. Use `Boundary` to
separate important code from background areas. Add `State` or `Causality` only
when the requested behavior depends on them.

## Workflow

### 1. Establish The Understanding Goal

Determine what the human needs to do after understanding the repository. A
goal such as "change authentication" or "trace evaluation scoring" is more
useful than "explain everything."

State the repository's purpose in plain language and identify the system
boundary relevant to that goal.

### 2. Build A Structural Inventory

Use high-signal artifacts to identify major components and entry points. Treat
directory names as hints until code, configuration, or documentation confirms
their responsibility.

Classify generated, vendored, test, tooling, and runtime code so they are not
mistaken for equal architectural peers.

### 3. Apply Repository Top-Down Levels

Descend through these scenario-specific levels:

```text
repository purpose
  -> major components
  -> component responsibilities and boundaries
  -> goal-relevant execution paths
  -> key files and contracts
  -> key functions or local mechanisms
```

Do not descend every branch. At each level, explain which branch matters to the
goal and which siblings can remain background context.

### 4. Trace Representative Paths

Select the smallest set of paths that demonstrates how the relevant behavior
works. Start from a real entry point and label transitions using control, data,
state, configuration, or ownership relationships.

Explain why each destination is visited. Do not substitute a list of files for
an execution model.

### 5. Identify Boundaries And Extension Points

Explain:

- where public contracts meet internal implementation;
- where state or data changes ownership;
- where configuration changes behavior;
- where tests or adapters define expected use;
- where a future change relevant to the goal should begin.

Mention architectural uncertainty when observed code and documentation differ.

### 6. Stop At Useful Depth

Descend into functions only when their mechanisms change the human's
understanding or next action. Re-anchor local details to their component and
repository responsibility.

**Depth gate:** stop when the human can locate the relevant path and predict
where a goal-related change or investigation belongs.

### 7. Synthesize The Mental Model

Communicate the repository as a connected model:

```text
purpose -> responsibilities -> relevant path -> implementation anchors -> next action
```

Include ignored areas and why they are not currently important.

## Allowed Iteration

- A discovered runtime edge may revise the component map.
- A misleading directory or stale document must be corrected using stronger
  source evidence.
- Expand to another path only when the first cannot explain a required
  behavior or boundary.
- Do not continue reading files merely to increase coverage.

## Stopping Conditions

Complete when the human can:

- state the repository's purpose;
- name the major relevant responsibilities and boundaries;
- trace the path tied to their goal;
- identify key files or contracts for deeper work;
- distinguish facts, inferences, and unexplored areas.

Stop as blocked when the repository is incomplete, generated without source, or
missing the entry points required to support a reliable model.

## Output Contract

The final response must make recoverable:

- a one-sentence repository purpose;
- the important components and responsibilities;
- why selected components matter to the goal;
- one or more labeled execution or data paths;
- key files, contracts, and implementation anchors;
- areas intentionally not explored and why;
- unknowns, contradictions, and the recommended next starting point.

This is a content contract, not a fixed section template.

## Quality Gate

Before finishing, confirm:

1. the explanation is organized around the human's goal;
2. component responsibilities are evidence-backed;
3. selected paths begin at real entry points;
4. transitions explain relationships, not only destinations;
5. irrelevant siblings are bounded rather than described equally;
6. local implementation is reconnected to repository purpose;
7. the human could navigate the relevant code without repeating the full exploration.
