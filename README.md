# Shit Skill

Shit Skill is a composable work protocol for turning an AI's broad task context
into a mental model a lower-context human can follow and use.

Its core idea is:

> Explain the path, not just the nodes.

The name points to a serious workflow property: even a simple outcome depends
on prerequisites being satisfied in the right order. The skill makes those
prerequisites, transitions, causal links, and checks explicit.

## Architecture

```text
ShitSkill/
├── SKILL.md
├── rules/       # What must always be true?
├── modules/     # What reusable method can achieve it?
└── scenarios/   # How are methods and rules composed for this task?
```

| Layer | Owns | Must Not Own |
| --- | --- | --- |
| Rules | Atomic, scenario-independent behavioral constraints. | Procedures or task-specific workflows. |
| Modules | Reusable methods with inputs, procedures, outputs, and quality gates. | Branches based on scenario names. |
| Scenarios | Goal-oriented composition, ordering, gates, and output contracts. | Copies of module or rule content. |

Workflow is part of a scenario rather than a fourth top-level layer.

## First-Version Scope

Implemented:

- 14 atomic rules covering context, navigation, scope, explanation, evidence,
  causality, and verification.
- Six reusable modules: `better-understanding`, `better-explanation`,
  `top-down`, `path-navigation`, `causal-reasoning`, and `verification`.
- Seven executable scenario workflows and a shared scenario contract.
- A top-level TRAE skill router.

Implemented scenarios:

1. [`bug-fix`](scenarios/bug-fix/SCENARIO.md)
2. [`code-review`](scenarios/code-review/SCENARIO.md)
3. [`repo-understanding`](scenarios/repo-understanding/SCENARIO.md)
4. [`module-development`](scenarios/module-development/SCENARIO.md)
5. [`debugging`](scenarios/debugging/SCENARIO.md)
6. [`document-understanding`](scenarios/document-understanding/SCENARIO.md)
7. [`architecture-understanding`](scenarios/architecture-understanding/SCENARIO.md)

See [the rule index](rules/README.md), [the module roadmap](modules/README.md),
and [the scenario catalog](scenarios/README.md).

## Design Source

This version follows the architecture agreed in the shared discussion
[“设计shit skill”](https://chatgpt.com/share/6a8ab070-43c4-83ee-868c-052316b860e5):

```text
Rule     -> What must be true?
Module   -> How can we achieve it?
Scenario -> How do we compose it here?
```
