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
3. [`better-explanation`](../../modules/better-explanation/MODULE.md)

Apply these rules:

- [Context rules](../../rules/context-rules.md): Assume Limited Human Context,
  Establish Context First, Progressive Disclosure.
- [Navigation rules](../../rules/navigation-rules.md): Explain Non-Obvious
  Transitions, Explain Why It Matters, Stay Goal-Relevant, Maintain Zoom
  Coherence.
- [Explanation rules](../../rules/explanation-rules.md): Introduce Terms In
  Plain Language, Prefer Causal Relationships, Preserve Causal Order,
  Distinguish Fact From Inference, Cite Original Evidence.

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

### 4. Build A Concept Map

For each essential concept, capture its plain-language role, precise meaning in
the document, and relation to other concepts. Resolve pronouns, overloaded
terms, and implied prerequisites that would otherwise break the explanation.

Do not expand terminology unrelated to the human's goal.

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

### 6. Explain Rationale And Boundaries

Identify why the proposed model, process, or decision exists; what alternatives
or constraints it addresses; where it applies; and where it does not.

Use examples to ground the model only after the relevant concepts are defined.

### 7. Synthesize For The Human's Goal

Reconnect the document's concepts and conclusions to the human's intended use.
State what must be remembered, what can be looked up later, and which claims
remain ambiguous or unsupported.

## Allowed Iteration

- Return to a definition when a later section changes its meaning.
- Consult a referenced source only when the current document depends on it for
  a material claim.
- Compare another document only when the human requests comparison or a
  contradiction blocks understanding.
- Do not replace source fidelity with a generic explanation of the topic.

## Stopping Conditions

Complete when the human can explain:

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
- its central model or claim;
- essential terms in plain language and precise context;
- relationships and overall flow;
- rationale, tradeoffs, and applicability boundaries;
- a concrete example when it materially aids understanding;
- actionable conclusions and unresolved ambiguities;
- source location references when available.

This is a content contract, not a generic summary template.

## Quality Gate

Before finishing, confirm:

1. the explanation reflects the document rather than generic domain knowledge;
2. key terms are defined before being relied upon;
3. relationships and logical transitions are explicit;
4. source claims and interpretation remain distinguishable;
5. examples preserve the source's constraints;
6. irrelevant sections do not receive equal depth;
7. the human can state what the document means and how to use it.
