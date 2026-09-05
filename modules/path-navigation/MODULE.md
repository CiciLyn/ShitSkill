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
  ownership, configuration, registration and lookup mechanisms, subprocess or
  protocol boundaries, logs, or documentation links.
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

When an object or value crosses the transition under a different source
identifier, record both exact names and the operation connecting them:

```text
caller: self.config_path
  -- passed positionally to -->
callee: load_config(config_path)
  -- referenced in the callee as -->
config_path
```

Do not use one identifier while citing lines whose scope contains only the
other identifier.

### 5. Complete Concrete Execution Paths

When the claim concerns what code does at runtime, continue past the first
relevant function until the path reaches the observable operation or the
system boundary that controls it. Resolve intermediate indirection rather than
compressing it into a conceptual arrow, including when applicable:

- framework accessors, registries, service-name lookups, dependency injection,
  dynamic dispatch, and adapter or wrapper methods;
- the object or value selected at each lookup and where that object came from;
- command construction, subprocess creation, namespace entry, transport calls,
  persistence, or external API boundaries;
- the return path when it changes the caller's behavior or the final result.

Represent the result as a synthesized invocation chain whose hops use precise
runtime verbs:

```text
entry()
  -> looks up service_name in the current runtime map
ServiceEnvironment.exec()
  -> delegates the command to
Container.exec()
  -> enters the target execution context and starts
subprocess / protocol operation
  -> produces
observable effect
```

For every retained hop, attach the implementation excerpt that proves the edge,
or mark the hop as inferred and name the missing evidence. A citation to only
the first and last function is not an end-to-end trace. Keep an invocation
chain distinct from a causal chain: the former proves how execution travels;
the latter explains why those operations produce the observed outcome.

**Depth evidence gate:** before descending to another helper, file, process, or
service, verify that every retained hop at the current depth has its own source
anchor and exact identifier mapping. If not, repair the ledger or stop at the
gap; do not let citations disappear as the explanation gets deeper.

### 6. Control Branching

When several outgoing edges are available:

1. rank them by relevance to the navigation question;
2. follow the smallest set that can answer it;
3. note obvious alternatives that were excluded;
4. explain why an excluded branch is currently lower value.

Explore a second branch only when the first branch is disproved, incomplete, or
insufficient to distinguish competing explanations.

### 7. Handle Dead Ends And Loops

If a path stops producing evidence, mark the dead end and return to the last
supported branch point. If the path revisits a node, state what new question or
evidence justifies the revisit.

Do not silently jump to an unrelated path.

### 8. Stop At A Decision-Relevant Node

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
Concrete execution chain:
Identifier mappings:
Evidence per hop:
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
3. concrete runtime claims are traced through dynamic lookup, wrappers, and
   execution boundaries to an observable effect;
4. every implementation-specific hop has a source anchor or explicit evidence
   gap;
5. the reason for choosing each next node is explicit;
6. excluded branches and dead ends are accounted for when material;
7. the path stops for a stated decision-relevant reason;
8. facts and inferred links remain distinguishable.
