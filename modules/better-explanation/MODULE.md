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

### 5. Make Quantitative Reasoning Mentally Executable

When a conclusion depends on an equation, statistical relation, threshold, or
condition, explain the model before asking the human to interpret the notation.
An equation is a compressed statement of a relationship, not an explanation of
why that relationship holds.

Build the explanation in this order:

1. State the concrete quantity being explained and its unit.
2. Identify one observation or experimental unit and what can vary between
   observations.
3. Define every symbol in plain language, including whether it is an observed
   value, an estimate from available data, or an unknown population quantity.
4. Explain the mechanism in words before presenting the equation.
5. State the assumptions required for that mechanism and identify which step
   uses each assumption.
6. Give the equation, substitute concrete values when available, and interpret
   the result in the original unit.
7. State what the calculation supports, what it does not establish, and how the
   conclusion changes when an assumption fails.

For an averaging example, establish the model before showing the relation:

- `D_i` is the signed difference measured on observation `i`, such as one
  case's score difference in score points;
- `i` labels an observation, and `n` is the number of observations being
  averaged;
- `mu` is the unknown population mean of `D_i`: the long-run signed difference
  expected across repeated observations;
- `D_bar_n` is the sample-mean statistic produced from `n` observations; it
  varies across repeated samples, and the number computed from the current data
  is one observed realization in the same unit as `D_i`;
- `SD(X)` means the standard deviation of quantity `X`: take each repeated
  value's distance from the long-run mean, square those distances, average
  them, and take the square root; the result has the same unit as `X`;
- `sigma = SD(D_i)` is therefore the population standard deviation of one
  observation, in score points in this example.

Then explain the mechanism. Each observation has a residual `D_i - mu`, which
is its positive or negative departure from the long-run mean. If observations
are independent and have the same spread, those residuals do not move together.
On the squared-spread scale, their contributions add: the sum of `n`
observations has squared spread `n * sigma^2`. Forming an average divides the
sum by `n`, so its squared spread is divided by `n^2`, leaving `sigma^2 / n`.
Converting squared spread back to standard deviation gives `sigma / sqrt(n)`.
Only after that explanation is the compact notation meaningful:

```text
D_bar_n = (D_1 + ... + D_n) / n
SD(D_bar_n) = sigma / sqrt(n)
```

The equality is exact for independent observations with the same `sigma`.
Under weak dependence or unequal but comparable spreads, `1 / sqrt(n)` may be
only an approximation; positive correlation makes averaging reduce noise more
slowly and is better described with a smaller effective sample size.

Name assumptions narrowly instead of attaching them to the whole argument.
Separate:

- a mathematical consequence that follows once a model is accepted;
- a modeling assumption such as independence or comparable variance;
- an empirical condition claimed to hold in the current data;
- a simplifying hypothesis used only to estimate an order of magnitude.

Every phrase such as "when the mean is near zero", "assuming independence", or
"for a sufficiently large sample" needs condition provenance:

```text
condition
  -> precise meaning
  -> evidence, derivation, or explicit assumption
  -> step that requires it
  -> consequence if it is false
```

Treat "the mean is near zero" as a separate empirical claim, not as a
consequence of averaging. First define what "near" means in the original unit.
For example, if differences smaller than `epsilon = 0.5` score points are
operationally negligible, the claim is `abs(mu) <= epsilon`, where `mu` is the
unknown population mean, not the observed `D_bar_n`.

Then identify evidence for that claim. Relevant empirical support could be an
uncertainty interval for `mu`, based on adequate independent observations, that
lies entirely inside `[-epsilon, epsilon]`. A design or domain symmetry may
justify using zero-centering as a modeling assumption, but it does not prove
the actual `mu` is near zero. A single small `D_bar_n`, a roughly balanced win
count, a large `n`, or a confidence interval that merely crosses zero does not
establish that `mu` is near zero. If sufficient evidence is unavailable, state
`abs(mu) <= epsilon` as an assumption and keep the conclusion conditional on
it.

Be exact about why a condition matters. The relation
`SD(D_bar_n) = sigma / sqrt(n)` does not require `mu` to be zero: it describes
spread around whatever `mu` is. A near-zero `mu` is needed only when that
spread is being used as a proxy for the typical absolute observed gap from
zero. If `abs(mu) > epsilon`, larger samples shrink random variation around
`mu`, but the systematic gap remains.

Use a concrete contrast when it resolves the abstraction. For example, if
single-case differences have a spread of 10 points and no persistent signed
direction, averaging 10 cases has a random scale of about `10 / sqrt(10) = 3.2`
points, while averaging 100 cases has a scale of about 1 point. If one system
instead has a persistent 4-point disadvantage, more cases narrow the noise
around that disadvantage; they do not make the 4-point gap disappear.

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

### 7. Bind Source-Dependent Claims To Evidence

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

### 8. Control Cognitive Load

Group related details under one claim, keep evidence adjacent to that claim,
and omit irrelevant branches. When an omitted branch is an obvious alternative,
state briefly why it does not matter.

Use examples only when they resolve an abstraction or demonstrate a
relationship; examples must not become a second unexplained system.

### 9. Close The Loop

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
3. concrete runtime behavior is shown through the established invocation chain
   to its observable effect or relevant boundary;
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
