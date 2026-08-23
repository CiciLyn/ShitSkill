# Verification

## Purpose

Design proportionate checks for important claims or actions and report what the
result proves, does not prove, and leaves at risk.

This module determines **how to establish confidence in an outcome**. A scenario
chooses the domain-specific tools and execution constraints.

## Inputs

- The goal and completion condition.
- Claims, actions, or proposed decisions that require evidence.
- Expected outcomes and invariants.
- Falsifying observations, when available.
- Risk, blast radius, available tools, and environmental constraints.
- Existing evidence and known gaps.

## Method

### 1. Enumerate Verifiable Claims

Translate the intended outcome into explicit claims. Include:

- the primary behavior or conclusion;
- restored or preserved invariants;
- important negative claims, such as an unaffected boundary;
- material assumptions.

Do not verify only that an action executed; verify the outcome it was meant to
produce.

### 2. Match Evidence To Each Claim

For every claim, choose the smallest check capable of falsifying it. Depending
on the scenario, evidence may include:

- direct inspection or static analysis;
- focused automated checks;
- integration or end-to-end behavior;
- controlled experiments;
- runtime observations, logs, or metrics;
- independent source comparison.

Use broader checks when the risk or blast radius crosses boundaries. Do not use
a weak proxy when the claimed outcome requires stronger evidence.

### 3. Define Expected Observations

Before running or collecting evidence, state:

- the expected observation if the claim is correct;
- the observation that would falsify it;
- environmental prerequisites;
- ambiguity that could make the result inconclusive.

This prevents a successful command from being mistaken for a successful
outcome.

### 4. Execute Or Collect

Run the selected checks when the scenario and environment allow it. Preserve
the relevant command, input, version, scope, and result.

When execution is unavailable, say that the check was not run and identify the
best available substitute. Never invent evidence.

### 5. Classify Results

Assign each claim one status:

- **Passed**: observed evidence supports the claim at the required scope.
- **Failed**: observed evidence contradicts the claim.
- **Inconclusive**: a check ran but cannot distinguish the relevant outcomes.
- **Not run**: no direct check was performed.

Explain what a passing result does not cover when the boundary matters.

### 6. Check Impact And Boundaries

Verify both the intended path and material neighboring behavior. Scale this
work according to:

- shared interfaces or contracts;
- state and data migration risk;
- concurrency or timing sensitivity;
- security or permission boundaries;
- user-visible blast radius;
- reversibility.

Do not claim that unrelated behavior is unaffected without evidence or a clear
structural argument.

### 7. Report Residual Confidence

Summarize:

- claims supported by direct evidence;
- failed, inconclusive, or unrun checks;
- environmental limitations;
- residual risks;
- the next check that would most increase confidence.

Success language must match the strongest completed evidence, not the intended
outcome.

## Verification Matrix

Maintain this compact internal artifact:

```text
Claim:
Risk:
Check:
Expected observation:
Falsifying observation:
Observed result:
Status: passed | failed | inconclusive | not run
Coverage:
Gap:
```

Use one entry per material claim. This is an evidence contract, not a mandatory
user-facing table.

## Non-Goals

This module does not:

- define scenario-specific commands or test suites;
- equate command exit code with behavioral correctness;
- require exhaustive verification for every low-risk claim;
- hide checks that failed or could not run;
- guarantee correctness beyond the observed evidence.

## Quality Gate

The module is complete when:

1. every material claim has a proportional check or an explicit gap;
2. expected and falsifying observations were defined;
3. results are classified as passed, failed, inconclusive, or not run;
4. evidence scope matches the confidence language;
5. material impact boundaries were considered;
6. residual risks and the highest-value next check are explicit.
