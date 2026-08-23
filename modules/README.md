# Module Roadmap

Modules answer one question: **what reusable method helps satisfy the rules?**

A module defines a method, its inputs, outputs, procedure, boundaries, and
quality checks. It must remain independent of any one task scenario.

| Module | Responsibility | Status |
| --- | --- | --- |
| [`better-understanding`](better-understanding/MODULE.md) | Build a goal-relevant mental model for a human with limited context. | Implemented |
| [`better-explanation`](better-explanation/MODULE.md) | Turn an established mental model into a clear, progressively disclosed explanation. | Implemented |
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
- Progressive disclosure remains a rule. `better-explanation` defines a
  reusable method for applying it.
- `top-down` is a reusable module, while each scenario decides what its levels
  mean and when to descend.
- Goal-oriented ordering belongs to scenario workflows rather than a generic
  orchestration module.
- Modules do not import rules, select rules, or direct other modules.
- Scenarios select rules, import and order modules, and own handoffs and
  iteration; modules never branch on scenario names.
