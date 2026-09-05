# Module Roadmap

Modules answer one question: **what reusable method helps satisfy the rules?**

A module defines a method, its inputs, outputs, procedure, boundaries, and
quality checks. It must remain independent of any one task scenario.

| Module | Responsibility | Status |
| --- | --- | --- |
| [`better-understanding`](better-understanding/MODULE.md) | Build a goal-relevant mental model and externalize non-trivial relationships visually. | Implemented |
| [`breadth-depth-explanation`](breadth-depth-explanation/MODULE.md) | Map all relevant nodes shallowly, then explain at most three nodes deeply per turn while preserving exact identifiers and the remaining queue. | Implemented |
| [`better-explanation`](better-explanation/MODULE.md) | Explain clearly and continually earn a low-context reader's attention. | Implemented |
| [`top-down`](top-down/MODULE.md) | Descend from the highest relevant abstraction to implementation detail without losing orientation. | Implemented |
| [`path-navigation`](path-navigation/MODULE.md) | Trace and explain meaningful transitions across artifacts, components, and abstraction levels. | Implemented |
| [`causal-reasoning`](causal-reasoning/MODULE.md) | Connect observations, causes, decisions, actions, and consequences with evidence. | Implemented |
| [`verification`](verification/MODULE.md) | Design proportionate checks and report evidence, gaps, impact, and residual risk. | Implemented |

## Boundary Decisions

- Context establishment and mental-model construction belong to
  `better-understanding`; they are not separate modules until they need an
  independent lifecycle.
- `better-understanding` defines the mental-model primitives and construction
  method; each scenario selects the primitives required by its task.
- `breadth-depth-explanation` owns the per-turn breadth map, active-node budget,
  identifier mapping, and visible continuation checkpoint; it does not limit
  internal investigation or implementation.
- Progressive disclosure remains a rule. `better-explanation` defines a
  reusable method for applying it.
- Visual-model construction belongs to `better-understanding`; presentation,
  labeling, and explanation of that model belong to `better-explanation`.
- Sentence-level analogy is an explanation method, not a source of evidence or
  a substitute for the real mechanism.
- Keeping the reader's attention belongs to `better-explanation`; it earns
  continued reading through relevance and progress rather than suspense or
  decoration.
- `top-down` is a reusable module, while each scenario decides what its levels
  mean and when to descend.
- Goal-oriented ordering belongs to scenario workflows rather than a generic
  orchestration module.
- Modules do not import rules, select rules, or direct other modules.
- Scenarios select rules, import and order modules, and own handoffs and
  iteration; modules never branch on scenario names.
