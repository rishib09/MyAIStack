---
id: W-001
feature: F-001
modules: [M-002, M-003]
chosen_design: D-A
status: draft | ready | in-progress | done | dropped
---

# W-001 <Scenario name>

## Source intent   <!-- only when this item was filed directly from a user request -->
- Request: <the user's words, verbatim>
- Requirement: <the request restated as a functional requirement>
- Approved by user: <yes, date>

## Trigger and input
<What starts this scenario. Example input.>

## Expected outcome
<What the user sees or gets.>

## Design options
<Exactly one row is chosen. A rejected row stays one line: no steps, libraries, risk areas or tests.>

| ID | Design | Status | Reason |
|----|--------|--------|--------|
| D-A | <one line> | chosen | <why it was chosen> |
| D-B | <one line> | rejected | <why it was rejected> |

## Chosen design: D-A
- Pattern: <design pattern name and one-line description>
- Frameworks or libraries: <names, and how each follows the project's coding standards>
- Steps:
  1. [M-xxx] <step>
  2. [M-xxx] <step>

## Contract
- Input: <shape and constraints>
- Output: <shape and constraints>
- Invariants: <must always hold, for example "every node emits a trace span">

## Failure paths
- <Condition> → <expected handling>

## Risk areas
<Derived from the chosen design only.>

| Design choice | Strength | Weakness → risk area |
|---------------|----------|----------------------|

## Workflow tests (black-box)
| ID | Risk area | Prompt or input | Pass condition | Metric ≥ threshold | Intent | Kind |
|----|-----------|-----------------|----------------|--------------------|--------|------|
| WT1 |  |  |  |  | functional / adversarial | single-turn / multi-turn |

Adversarial waiver: none | <reason, approved by user on date>

## Work items
| ID | Type | Title | Module | Status |
|----|------|-------|--------|--------|
| T-001 | task / bug |  | M-xxx |  |
