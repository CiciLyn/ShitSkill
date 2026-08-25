# Rules

Rules answer one question: **what must remain true in every scenario?**

Each rule is deliberately one sentence, but related rules share a document. A
rule constrains behavior; it does not describe a procedure. Reusable procedures
belong in `modules/`, while task-specific ordering belongs in `scenarios/`.

## Rule Documents

- [Context rules](context-rules.md): human context, initial orientation, and
  progressive disclosure.
- [Navigation rules](navigation-rules.md): transitions, importance, relevant
  scope, and coherent zoom levels.
- [Explanation rules](explanation-rules.md): terminology, accessible
  mathematics, causality, evidence, epistemic status, source citation, change
  intent, and verification.

## Selection

Scenarios should import the documents relevant to their workflow and name the
specific rules they apply. `Assume Limited Human Context` is the default
foundation for every scenario. Scenario files may specialize how a rule is
applied, but must not redefine or duplicate it.
