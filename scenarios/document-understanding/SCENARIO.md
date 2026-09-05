# Document Understanding Scenario

## Trigger

Use this scenario when the human asks to understand, summarize, compare, or
explain a technical document, specification, design, paper, or policy.

Route to `architecture-understanding` when the primary task is reconstructing a
system architecture from multiple sources. Route to `code-review` when the
document is only supporting evidence for reviewing a code change.

## Goal

Build a faithful mental model of the document's problem, concepts,
relationships, argument or process, design rationale, and actionable
conclusions.

## Imports

Read and apply these modules in workflow order:

1. [`better-understanding`](../../modules/better-understanding/MODULE.md)
2. [`top-down`](../../modules/top-down/MODULE.md)
3. [`breadth-depth-explanation`](../../modules/breadth-depth-explanation/MODULE.md)
4. [`better-explanation`](../../modules/better-explanation/MODULE.md)

Apply these rules:

- [Context rules](../../rules/context-rules.md): Assume Minimal Human Context,
  Assume No Prerequisite Knowledge, Respect Limited Patience, Establish Context
  First, Progressive Disclosure.
- [Navigation rules](../../rules/navigation-rules.md): Explain Non-Obvious
  Transitions, Explain Why It Matters, Stay Goal-Relevant, Maintain Zoom
  Coherence, Map Breadth Before Depth, Limit Deep-Dive Nodes Per Turn,
  Preserve Explanation State, Maintain Evidence Through Depth.
- [Explanation rules](../../rules/explanation-rules.md): Introduce Terms In
  Plain Language, Expand Compressed Language, Preserve Source Identifiers,
  Label Explanatory Names, Declare Identifier Remapping, Use Sentence-Level
  Analogies, Visualize Non-Trivial Relationships, Earn Continued Attention,
  Make Quantitative Reasoning Executable, Prefer Causal Relationships,
  Preserve Causal Order, Distinguish Fact From Inference, Cite Original
  Evidence.

## Inputs

- The source document and its version or publication context.
- The human's question, intended use, and existing familiarity.
- Document structure, definitions, examples, diagrams, references, and claims.
- Related sources only when needed to resolve an explicit dependency or
  contradiction.

## Understanding Model

Select models from the document type:

- contract or design: `Structure`, `Responsibility`, and `Boundary`;
- process or tutorial: `Flow / sequence`, with `State` when lifecycle matters;
- argument or evidence report: `Causality`, with `Structure` for its claims.

Use only the combination needed by the human's question.

## Workflow

### 1. Establish Purpose And Scope

Identify what problem the document addresses, who it is for, what decision or
behavior it seeks to influence, and what the human wants to learn from it.

Separate the document's stated scope from assumptions about the broader topic.

**Source gate:** do not present a faithful-document interpretation unless the
relevant source content and its version or context are available. If only an
excerpt is available, bound conclusions to that excerpt.

### 2. Identify The Document Type

Determine whether the document primarily defines a contract, proposes a design,
describes a process, reports evidence, argues for a decision, or teaches a
concept. Use that type to identify what constitutes the document's core logic.

### 3. Apply Document Top-Down Levels

Descend through these scenario-specific levels:

```text
problem and intended outcome
  -> central claim or governing model
  -> key concepts
  -> relationships among concepts
  -> process, argument, or mechanism
  -> rationale and tradeoffs
  -> examples and edge conditions
  -> actionable conclusions
```

Skip levels that the document does not contain. Do not force a process document
into an argument structure or vice versa.

### 4. Build The Concept And Explanation Breadth Map

For each essential concept, capture its plain-language role, precise meaning in
the document, and relation to other concepts. Resolve pronouns, overloaded
terms, and implied prerequisites that would otherwise break the explanation.

Do not expand terminology unrelated to the human's goal.

Apply `breadth-depth-explanation` to include every goal-relevant concept, claim,
process step, rationale, and conclusion at shallow depth. Preserve canonical
document terms and exact source identifiers such as field or parameter names.

Select no more than three active nodes for the current response unless the
human explicitly requests one exhaustive pass. Keep the remaining nodes in the
visible queue.

**Breadth gate:** do not deeply reconstruct a concept, mechanism, or argument
until the complete goal-relevant shallow map and this turn's active nodes are
explicit.

### 5. Reconstruct The Logic

Trace how the document moves from premise or input to conclusion or output.
Distinguish:

- statements made directly by the source;
- conclusions implied by combining source statements;
- external interpretation or critique.

When the document omits a logical transition, mark the gap rather than filling
it silently.

**Interpretation gate:** before synthesizing conclusions, every material claim
must remain traceable to source text or be labeled as inference or external
context.

Deeply reconstruct only the active nodes for this turn, while allowing each
selected node to reach its conclusion, output, or applicability boundary.
Every retained source-dependent step must keep its source anchor and any
identifier mapping.

### 6. Explain Rationale And Boundaries

Identify why the proposed model, process, or decision exists; what alternatives
or constraints it addresses; where it applies; and where it does not.

Use examples to ground the model only after the relevant concepts are defined.

### 7. Synthesize For The Human's Goal

Reconnect the document's concepts and conclusions to the human's intended use.
State what must be remembered, what can be looked up later, and which claims
remain ambiguous or unsupported.

When queued nodes remain, close with the visible checkpoint from
`breadth-depth-explanation` instead of continuing into another deep-dive group.

## Allowed Iteration

- Return to a definition when a later section changes its meaning.
- A follow-up about an active node may deepen that node without consuming a
  queued node.
- Consult a referenced source only when the current document depends on it for
  a material claim.
- Compare another document only when the human requests comparison or a
  contradiction blocks understanding.
- Do not replace source fidelity with a generic explanation of the topic.

## Stopping Conditions

The current explanation turn is complete when the selected active nodes reach
useful depth, every retained source-dependent step keeps its evidence, and
explained, follow-up, and remaining nodes are visible.

The whole topic is complete when no goal-relevant nodes remain queued and the
human can explain:

- the problem and intended outcome;
- the essential concepts and relationships;
- the main process, mechanism, or argument;
- the rationale, boundaries, and conclusions;
- which statements are source facts, inferences, or unresolved gaps.

Stop as blocked when material sections, referenced definitions, or source
access are missing and prevent faithful interpretation.

## Output Contract

The final response must make recoverable:

- what the document is trying to accomplish;
- the complete shallow breadth map and the active nodes selected for this turn;
- its central model or claim;
- essential terms in plain language and precise context;
- exact source identifiers and mappings where the document changes names;
- relationships and overall flow;
- rationale, tradeoffs, and applicability boundaries;
- a concrete example when it materially aids understanding;
- actionable conclusions and unresolved ambiguities;
- source location references when available;
- a continuation checkpoint when nodes remain.

This is a content contract, not a generic summary template.

## Quality Gate

Before finishing, confirm:

1. the explanation reflects the document rather than generic domain knowledge;
2. key terms are defined before being relied upon;
3. relationships and logical transitions are explicit;
4. source claims and interpretation remain distinguishable;
5. examples preserve the source's constraints;
6. irrelevant sections do not receive equal depth;
7. no more than three nodes received deep treatment unless the human requested
   an exhaustive pass;
8. exact source identifiers and evidence survive every retained deep step;
9. the remaining explanation queue is visible when the whole topic is not yet
   complete;
10. the human can state what the document means and how to use it.
