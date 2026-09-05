# Better Explanation

## Purpose

Turn an established mental model into an explanation for a human who may have
little context, little familiarity with the domain, and little patience.

This module determines **how to communicate what is already understood**. It
does not establish truth, choose the task workflow, or replace missing evidence.

## Inputs

- A goal-relevant mental model.
- The human's demonstrated context, domain familiarity, and requested depth.
- Facts, inferences, unknowns, and supporting evidence.
- Precise locations and verbatim excerpts for source-dependent claims.
- Complete invocation paths and evidence for each retained hop when concrete
  runtime behavior is being explained.
- Exact source identifiers, identifier mappings across scopes, and any
  explanation checkpoint that must survive into a later turn.
- Important relationships and transitions.
- The outcome or decision the explanation must support.
- Competing demands on the human's attention and the earliest point at which
  they gain something useful.

If the mental model is incomplete, report the missing input instead of hiding
the gap with polished prose.

## Method

### 1. Set The Entry Point

Begin with the smallest orientation that makes the remaining explanation
meaningful:

- the question and direct answer or current outcome;
- the system location;
- the central conclusion, when already supported.

Do not delay the useful point with ceremony, a deep implementation detail, or
unexplained terminology. If a detour is required before the answer, say what
question the detour resolves and why the answer depends on it.

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

### 4. Earn And Re-Earn Attention

Treat attention as conditional, not as something the explanation owns after the
first sentence. Every substantial section must make three things clear:

- the question this section answers;
- why that question matters at this point in the explanation;
- what new understanding, evidence, prediction, or decision the human gains.

The visible response does not need to label these three points, but the reader
must be able to see that their understanding is increasing. Give a useful
result before asking for more effort. When a dense technical passage is
necessary, first state what it will establish, then reconnect its result to the
original goal immediately afterward.

Do not confuse brevity with attention. Missing context forces the reader to do
extra reconstruction work, so keep necessary context and place it immediately
before the detail that needs it.

Use headings, concrete examples, representative runs, and visuals when they
reduce the effort required to see relevance or progress. Do not use them as
decoration.

Before finishing, check whether the writing keeps earning attention:

1. Does the opening reveal the answer, current state, or next useful question?
2. Does each section show why it belongs before presenting its detail?
3. Does each section change the human's understanding, confidence, or action?
4. Can a paragraph be removed without weakening the explanation? If so, remove
   it.
5. Is a section's useful result delayed until its end? If so, move enough of
   that result forward to justify the reading effort.
6. After dense detail, is the human re-anchored to the goal and the progress
   just made?

Never manufacture suspense, hide the answer to force continued reading, use
clickbait, or add novelty that does not improve understanding. Attention should
be earned by relevance and cumulative progress.

### 5. Expand Compressed Meaning

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

Compressed language also includes abbreviations, stacked nouns, invented
compound labels, nounified verbs, and metaphorical labels. Expand these into a
complete relationship before using the short form:

```text
actor -> action -> object -> immediate result -> why that result matters
```

For example, `runtime boundary ownership mismatch` forces the human to unpack
four nouns without knowing the claim. Prefer: `The worker creates the resource,
but the controller tries to delete it. Because the controller does not own that
resource, cleanup fails.` The shorter label may be introduced afterward if it
will be reused.

For example, explaining that a network namespace is isolated is incomplete
unless the human also learns that it gives processes a separate set of
interfaces, routes, loopback endpoints, and firewall tables, and therefore
changes which service a command reaches. Likewise, naming a device path or
forwarding flag is not enough: explain what operation consumes it and what
specific path becomes unavailable when it is absent or disabled.

Before paraphrasing source, classify each technical name:

- an exact source identifier keeps its spelling and uses code formatting;
- a canonical source term keeps the source's spelling and capitalization;
- a plain-language explanation is written as a complete relationship;
- a reusable shorthand is explicitly introduced as explanatory shorthand and
  is not formatted as though it were a source identifier.

When a value changes names across scopes, show the exact mapping before using
the names in one explanation:

```text
constructor argument: llm_proxy_source_root
  -> stored on the instance as
self.llm_proxy_source_root
  -> passed to the context manager parameter
source_root
```

Do not silently replace all three identifiers with one preferred name. Each
name is valid only in the source scope where it appears.

### 6. Use Sentence-Level Analogies

Use an analogy when it makes an unfamiliar relationship easier to simulate
mentally. The analogy must be a short explanation, not a decorative noun:

1. State the unfamiliar mechanism.
2. Give a familiar situation with actors, actions, and consequences.
3. Map each relevant part of the familiar situation back to the real system.
4. State where the comparison stops being accurate.
5. Return to the precise technical term.

Avoid word-level analogies such as `the registry is a phonebook` or `the adapter
is glue`. They leave the human to invent the missing relationships and often
smuggle in false behavior.

Prefer a sentence-level analogy such as:

> A service registry works like a hotel front desk for named services: the
> caller asks for `billing`, the registry returns the service object currently
> assigned to that name, and the caller then invokes that object. Unlike a
> human receptionist, the registry follows exact registration and lookup rules;
> it does not decide which service is best.

An analogy explains a relationship; it is never evidence that the real
mechanism behaves that way.

### 7. Explain Mathematics Accessibly

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

### 8. Explain Relationships, Not Just Objects

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

### 9. Present The Visual Model

When the established mental model contains a non-trivial structure, branch,
interaction sequence, or state change, present its visual model near the first
explanation that depends on it.

Use this order:

1. one sentence naming the question the visual answers;
2. the Mermaid, ASCII, or tabular visual;
3. one sentence stating its main takeaway;
4. the evidence and detail needed to trust that takeaway.

Keep labels concrete and verbal: `controller asks worker to stop` communicates
more than `shutdown coordination`. A visual may compress layout, but it must
not compress meaning. Do not make the human infer unlabeled arrows, unexplained
abbreviations, or the difference between observed and hypothetical edges.

### 10. Instantiate One Representative Run

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

### 11. Bind Source-Dependent Claims To Evidence

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

### 12. Control Cognitive Load

Group related details under one claim, keep evidence adjacent to that claim,
and omit irrelevant branches. When an omitted branch is an obvious alternative,
state briefly why it does not matter.

Use examples only when they resolve an abstraction or demonstrate a
relationship; examples must not become a second unexplained system.

Before finishing, scan for sentences that require the human to unpack several
unknown terms or reconstruct a missing transition. Rewrite the sentence or add
the missing relationship. Do not respond to likely confusion by repeating the
same compressed wording.

### 13. Close The Loop

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
Reader assumptions still requiring support:
Goal:
Entry point:
Conceptual spine:
Key relationships:
What the reader gains near the opening:
What the reader gains from each substantial section:
Content to remove or move:
Visual model and takeaway:
Representative trigger and concrete values:
Invocation chain and evidence per hop:
Terms to expand:
Compressed phrases to rewrite:
Source-term classifications:
Identifier mappings:
Analogy mapping and limit:
Quantitative quantities, symbols, and units:
Quantitative mechanism and assumptions:
Condition provenance and failure cases:
Evidence placement:
Source anchors:
Explained nodes:
Remaining explanation queue:
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

1. the entry point gives the conclusion or next action that matters without
   requiring hidden context or unnecessary patience;
2. every important transition has an explicit relationship and reason;
3. concrete runtime behavior is shown through one representative run and the
   established invocation chain to its observable effect or relevant boundary;
4. unfamiliar terms include their mechanism, operational effect, and relevance
   at first meaningful use;
5. compressed phrases have been expanded into complete statements that name
   who acts, what they do, and what changes before their short forms are reused;
6. every analogy maps a complete relationship, names its limit, and remains
   distinct from evidence about the real system;
7. every non-trivial relationship has a readable visual model near its first
   use, or a specific reason why prose is clearer;
8. every material equation is preceded by a plain-language mechanism, defines
   every symbol and unit, and returns its result to the concrete quantity being
   explained;
9. every quantitative condition is identified as evidence, derivation, or
   assumption, with the step that needs it and the consequence if it fails;
10. population quantities, observed values, and estimates are not conflated;
11. every source-dependent claim has a nearby verbatim excerpt and precise
   location, or an explicit evidence gap;
12. behavioral and negative claims use implementation or runtime evidence when
   available instead of relying on documentation alone;
13. synthesized flows and pseudocode are distinguishable from original source;
14. details appear in a coherent progression rather than as disconnected facts;
15. the conclusion reconnects evidence and impact to the original goal;
16. facts, inferences, unknowns, and verification status remain distinguishable;
17. every substantial section earns continued attention through immediate
    relevance, visible progress, or a concrete gain without withholding the
    answer, removing necessary context, or adding decorative stimulation.
18. source identifiers remain exact and scoped, explanatory names are visibly
    labeled, and every cross-scope identifier change is mapped before use;
19. when the explanation continues across turns, explained nodes and the
    remaining queue are recoverable without reconstructing the topic.
