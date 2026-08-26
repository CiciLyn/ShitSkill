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
- Precise locations and verbatim excerpts for source-dependent claims.
- Complete invocation paths and evidence for each retained hop when concrete
  runtime behavior is being explained.
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
term
  -> plain-language role
  -> precise mechanism
  -> capability or state it controls
  -> concrete effect in this path
  -> relevance to the conclusion
```

Do not replace one unfamiliar term with several others. Reuse the precise term
after its meaning has been established. Treat kernel facilities, protocol
features, namespace types, device paths, configuration fields, and error-class
names as terms when the explanation depends on their behavior.

For example, explaining that a network namespace is isolated is incomplete
unless the human also learns that it gives processes a separate set of
interfaces, routes, loopback endpoints, and firewall tables, and therefore
changes which service a command reaches. Likewise, naming a device path or
forwarding flag is not enough: explain what operation consumes it and what
specific path becomes unavailable when it is absent or disabled.

### 5. Explain Mathematics Accessibly

Assume the human may have little mathematical background. Keep precise
mathematical terms when they are useful, but explain them in plain language at
first use instead of replacing them or expecting prior familiarity.

Use mathematics only when it makes the reasoning clearer. Prefer quantities
already present in the problem, and do not introduce a new variable merely to
make an explanation look formal.

When a new variable, equation, or mathematical condition is necessary:

1. Start with the concrete question and the unit being measured.
2. Introduce only the minimum symbols needed for that question.
3. Define each symbol at first use in plain language and tie it to the concrete
   thing it represents; distinguish observed values, estimates, and population
   quantities when that distinction affects the conclusion.
4. Show the formula or relationship that uses the symbol, explain each operation
   or relationship in words, and say whether it comes from a definition,
   derivation, empirical relationship, or approximation.
5. State every assumption and precondition used by the formula. For each one,
   explain what evidence makes it suitable for the current case. If that cannot
   be established, label it as an assumption or unknown instead of presenting
   it as fact.
6. Substitute concrete values when available and interpret the result in the
   original unit.
7. State what the calculation supports and how the conclusion changes if a
   premise does not hold.

Do not treat notation, a named theorem, or a formula as a substitute for the
plain-language explanation that lets the human reconstruct the reasoning.

### 6. Explain Relationships, Not Just Objects

For every non-obvious move from one item to another, state:

- what connects them;
- why the explanation moves there;
- what the destination contributes to the goal.

Prefer verbs such as calls, produces, validates, stores, constrains, or depends
on over unlabeled arrows.

When an established mental model contains a concrete execution path, render
the path without collapsing framework or operating-system indirection. Show
how a name or key resolves to an object, which method is dispatched, which
wrapper delegates next, which execution context is entered, and which command,
request, write, or return value creates the observable effect. Keep the chain
compact, but do not replace it with a citation to only the entry function.

### 7. Instantiate One Representative Run

When the human asks how several components work together, choose one concrete
trigger and carry it through the full path before giving a
component-by-component summary. At each handoff, name:

- the caller and callee;
- the actual runtime object, key, path, or state being transferred;
- why the callee is selected;
- what persistent or observable effect proves the handoff occurred;
- what is temporary, what survives, and who owns cleanup.

Use values from the current run when available. If only a hypothetical example
is possible, label it as hypothetical. Do not make the human mentally compose
an execution path from separate component descriptions.

### 8. Bind Source-Dependent Claims To Evidence

When a claim depends on concrete source behavior, bind it at first use to a
source anchor containing:

- the smallest verbatim excerpt that proves the behavior;
- a precise file and line range, plus a revision or diff identifier when the
  excerpt is no longer present in current source;
- one sentence explaining how the excerpt supports the claim.

Keep the source anchor next to the claim instead of deferring it to a distant
evidence section. A path-only citation is insufficient when the exact construct
is necessary to understand the behavior. A synthesized flow, pseudocode block,
or paraphrase may explain several source anchors, but label it as synthesis and
do not present it as original code.

Use evidence according to the claim:

- implementation source proves executable decisions and delegation;
- generated or deployed configuration proves the selected runtime inputs;
- runtime traces, logs, process state, packets, or metrics prove what happened
  in a particular execution;
- design documents and READMEs explain intended behavior and constraints.

Do not use documentation as the sole proof of actual behavior when the
responsible implementation or runtime evidence is available. A negative claim
such as "this path does not enable forwarding" needs evidence from the
responsible decision point or a bounded search of all relevant implementations,
not merely a document that says forwarding is unavailable.

For an invocation chain, place evidence at the hop it proves. The reader should
be able to distinguish, for example, a framework lookup from a method call and
a method call from a subprocess or network transition without trusting an
unanchored summary.

If the original source cannot be quoted or precisely located, state that
evidence gap where the claim first appears. Later references may link back to an
earlier source anchor instead of repeating the same excerpt.

For example, do not stop at:

```text
The caller serializes the body into the command. See path/to/file.py:L10-L18.
```

Show the decisive lines from that range, identify them as original source, and
then explain which values move into the command. The visible response need not
use a fixed template.

### 9. Control Cognitive Load

Group related details under one claim, keep evidence adjacent to that claim,
and omit irrelevant branches. When an omitted branch is an obvious alternative,
state briefly why it does not matter.

Use examples only when they resolve an abstraction or demonstrate a
relationship; examples must not become a second unexplained system.

### 10. Close The Loop

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
Representative trigger and concrete values:
Invocation chain and evidence per hop:
Terms to expand:
Quantitative quantities, symbols, and units:
Quantitative mechanism and assumptions:
Condition provenance and failure cases:
Evidence placement:
Source anchors:
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
3. concrete runtime behavior is shown through one representative run and the
   established invocation chain to its observable effect or relevant boundary;
4. unfamiliar terms include their mechanism, operational effect, and relevance
   at first meaningful use;
5. every material equation is preceded by a plain-language mechanism, defines
   every symbol and unit, and returns its result to the concrete quantity being
   explained;
6. every quantitative condition is identified as evidence, derivation, or
   assumption, with the step that needs it and the consequence if it fails;
7. population quantities, observed values, and estimates are not conflated;
8. every source-dependent claim has a nearby verbatim excerpt and precise
   location, or an explicit evidence gap;
9. behavioral and negative claims use implementation or runtime evidence when
   available instead of relying on documentation alone;
10. synthesized flows and pseudocode are distinguishable from original source;
11. details appear in a coherent progression rather than as disconnected facts;
12. the conclusion reconnects evidence and impact to the original goal;
13. facts, inferences, unknowns, and verification status remain distinguishable.
