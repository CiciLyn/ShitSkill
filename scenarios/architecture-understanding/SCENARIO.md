# Architecture Understanding Scenario

## Trigger

Use this scenario when the human needs to understand a system's boundaries,
components, responsibilities, interactions, invariants, or design tradeoffs.

Route to `repo-understanding` when the primary outcome is navigating one
repository's concrete structure. Route to `module-development` when the human
asks to implement an architectural change.

## Goal

Build an evidence-backed model of why the system is divided as it is, how its
parts collaborate on important flows, and what constraints and tradeoffs govern
change.

## Imports

Read and apply these modules in workflow order:

1. [`better-understanding`](../../modules/better-understanding/MODULE.md)
2. [`top-down`](../../modules/top-down/MODULE.md)
3. [`path-navigation`](../../modules/path-navigation/MODULE.md)
4. [`causal-reasoning`](../../modules/causal-reasoning/MODULE.md)
5. [`better-explanation`](../../modules/better-explanation/MODULE.md)

Apply these rules:

- [Context rules](../../rules/context-rules.md): Assume Minimal Human Context,
  Assume No Prerequisite Knowledge, Respect Limited Patience, Establish Context
  First, Progressive Disclosure.
- [Navigation rules](../../rules/navigation-rules.md): Explain Non-Obvious
  Transitions, Ground Relationships In One Concrete Scenario, Explain Why It
  Matters, Stay Goal-Relevant, Maintain Zoom Coherence.
- [Explanation rules](../../rules/explanation-rules.md): Introduce Terms In
  Plain Language, Expand Compressed Language, Use Sentence-Level Analogies,
  Visualize Non-Trivial Relationships, Earn Continued Attention,
  Make Quantitative Reasoning
  Executable, Prefer Causal Relationships, Preserve Causal Order,
  Distinguish Fact From Inference, Cite
  Original Evidence.

## Inputs

- The human's architectural question and desired decision.
- System boundaries, actors, repositories, services, data stores, and external
  dependencies.
- Design documents, deployment configuration, runtime paths, APIs, schemas,
  source, and operational evidence.
- Quality attributes and constraints such as reliability, latency, consistency,
  security, ownership, cost, and evolution.
- Current version and known differences between intended and actual architecture.

## Understanding Model

Use `Structure`, `Responsibility`, and `Boundary` for the architectural frame.
Add `Flow / sequence` for critical interactions, `State` for lifecycle or
consistency questions, and `Causality` for constraints, tradeoffs, and failure
propagation.

## Workflow

### 1. Define The Architectural Question

Identify the decision the model must support: orientation, change planning,
failure analysis, ownership, scaling, security, or tradeoff evaluation.

State the system's purpose and choose the smallest boundary that contains the
question.

**Boundary gate:** do not inventory components until the architectural question
and containing system boundary are explicit.

### 2. Establish Sources And Confidence

Rank evidence by authority and freshness. Compare intended architecture from
design documents with actual architecture shown by deployment, configuration,
interfaces, and runtime behavior.

Mark disagreement rather than silently choosing one source.

**Evidence gate:** architecture claims must be tied to intended-design evidence,
actual-system evidence, or labeled inference before they enter the model.
Claims about what a runtime path does or does not do require implementation,
deployed-configuration, or runtime evidence when available; documentation alone
establishes intent, not actual behavior.

### 3. Apply Architecture Top-Down Levels

Descend through these scenario-specific levels:

```text
system purpose and external actors
  -> system boundary and environment
  -> major components and ownership
  -> responsibilities and contracts
  -> critical interaction paths
  -> state, data, and control transitions
  -> invariants, quality attributes, and failure boundaries
  -> implementation anchors
```

Select only levels and branches needed for the architectural question.

### 4. Map Responsibilities And Boundaries

For each relevant component, explain:

- what responsibility it owns;
- what it deliberately does not own;
- its public contracts;
- state or data under its control;
- upstream and downstream dependencies.

Do not infer responsibility from component names alone.

### 5. Trace Critical Flows

Choose representative user, data, control, deployment, or failure flows. Label
each transition and explain why the next component participates.

Before generalizing the architecture, instantiate one representative trigger
with concrete runtime values. Carry the same example through lookup, object
construction, dispatch, execution, output, and cleanup so the human does not
have to infer how separately described components connect.

Show synchronous versus asynchronous boundaries, persistence points, trust
boundaries, and ownership changes when relevant.

For each concrete code path used to support an architectural conclusion, trace
the invocation through framework accessors, registries or named-object lookups,
adapter and wrapper methods, process or namespace transitions, and transport or
storage operations until it reaches the observable effect or relevant system
boundary. Bind every implementation-specific hop to the source excerpt that
proves it; do not cite only the entry function and summarize the intermediate
runtime machinery.

### 6. Explain Architectural Causes And Tradeoffs

Connect constraints to design decisions and consequences:

```text
constraint -> design decision -> gained property -> accepted cost or risk
```

Distinguish documented rationale from inferred rationale. Challenge claimed
benefits against actual implementation evidence.

### 7. Identify Invariants And Change Pressure

State which contracts or properties must remain stable, where failures are
contained or propagated, and which components are likely to change together.

Identify implementation anchors only after the architectural model is clear.

### 8. Synthesize The Model

Reconnect components and flows to the original architectural question. Explain
what the model supports confidently, where intended and actual architecture
diverge, and which evidence would resolve remaining uncertainty.

Define every architecture or operating-system term that carries causal weight
by stating its plain-language role, mechanism, controlled capability, effect on
the traced flow, and relevance to the conclusion.

## Allowed Iteration

- Runtime evidence may revise a document-derived component or flow.
- A critical path may cross the initial boundary; expand it only enough to
  explain the observed contract or consequence.
- Revisit a component when a newly discovered invariant changes its role.
- Do not enumerate every service, endpoint, or table unless the question
  requires exhaustive inventory.

## Stopping Conditions

Complete when the human can:

- state the system boundary and purpose;
- assign relevant responsibilities to components;
- trace the critical flows tied to the question;
- explain important constraints, invariants, and tradeoffs;
- identify evidence-backed implementation anchors and uncertainties.

Stop as blocked when authoritative architecture or runtime evidence is
inaccessible and competing system models cannot be reconciled.

## Output Contract

The final response must make recoverable:

- the architectural question, system purpose, and chosen boundary;
- relevant actors, components, responsibilities, and contracts;
- critical flows with labeled transitions, including an end-to-end invocation
  chain and implementation evidence per hop for concrete runtime behavior;
- state, data, control, trust, or failure boundaries when material;
- constraints, design decisions, benefits, costs, and risks;
- operational definitions for specialized terms whose mechanisms affect the
  conclusion;
- important invariants and change coupling;
- intended-versus-actual differences;
- implementation anchors, evidence sources, and unresolved uncertainty.

This is a content contract, not a fixed architecture document template.

## Quality Gate

Before finishing, confirm:

1. the system boundary matches the question;
2. responsibilities are supported by contracts or behavior;
3. concrete critical flows resolve runtime indirection and reach an observable
   operation or relevant system boundary with evidence for every retained hop;
4. implementation and negative behavioral claims do not rely on documentation
   alone when stronger evidence is available;
5. specialized terms explain both mechanism and effect in the current flow;
6. constraints are connected to design consequences;
7. documented and inferred rationale are distinguishable;
8. intended and actual architecture are not conflated;
9. the human can reason about the impact of a relevant change using the model.
