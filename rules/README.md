# Rules

Rules answer one question: **what must remain true in every scenario?**

Each rule is deliberately one sentence, but related rules share a document. A
rule constrains behavior; it does not describe a procedure. Reusable procedures
belong in `modules/`, while task-specific ordering belongs in `scenarios/`.

## Rule Documents

- [Context rules](context-rules.md): human context, prerequisite knowledge, patience, initial orientation, and
  progressive disclosure.
- [Navigation rules](navigation-rules.md): transitions, representative runtime
  scenarios, breadth-before-depth pacing, cross-turn explanation state,
  evidence continuity, relevant scope, and coherent zoom levels.
- [Explanation rules](explanation-rules.md): terminology, accessible
  mathematics, expanded language, source-identifier fidelity, explicit name
  remapping, sentence-level analogies, visual models, sustained attention,
  causality, evidence, epistemic status, source citation, change intent, and
  verification.

## Selection

Scenarios should import the documents relevant to their workflow and name the
specific rules they apply. `Assume Minimal Human Context`, `Assume No
Prerequisite Knowledge`, and `Respect Limited Patience` are the default reader
model for every scenario. Scenario files may specialize how a rule is applied,
but must not redefine or duplicate it.
