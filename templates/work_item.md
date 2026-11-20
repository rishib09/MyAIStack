---
id: T-001 | B-001
type: task | bug
parent: W-001 | F-001 | none
module: M-002
status: draft | ready | in-progress | in-review | done | dropped
---

# <Imperative title, one concern, no "and">

## Source intent   <!-- only when this item was filed directly from a user request -->
- Request: <the user's words, verbatim>
- Requirement: <the request restated as a functional requirement>
- Approved by user: <yes, date>

## Context
<1 to 3 lines: why this exists, linked to its parent.>

## Scope
- In: <files and components this item may change>
- Out: <files and components this item must not touch>

## Acceptance criteria
- <Verifiable check mapped to the parent's AC, contract or workflow test>

## Prescribed approach
<Required pattern, libraries, call path and conventions. Must match the parent workflow's chosen design. A reviewer checks the PR against this section.>

## Data structures and algorithms   <!-- only where the choice is not obvious -->
- <Choice> because <reason>. Rejected: <alternative> because <reason>.

## To-do
- [ ] <Exact step, in order>
- [ ] <...>

## Component tests (white-box)
| ID | Protects | Level | Interface | Mode | Intent | Test | Why this component |
|----|----------|-------|-----------|------|--------|------|--------------------|
| CT1 | W-xxx/WTn or contract line | unit / integration | backend / CLI / UI | auto / manual | functional / adversarial |  |  |

Adversarial waiver: none | <reason, approved by user on date>

## Bug details   <!-- bug only -->
- Violates: <F-xxx ACn or W-xxx contract line>
- Expected: <...>
- Actual: <...>
- Repro: <steps or input>
- Regression test: <name and location>

## Definition of done
- [ ] One PR
- [ ] Acceptance criteria pass
- [ ] Component tests pass, and the workflow tests they protect still pass
- [ ] Confirmed workflow tests unchanged
- [ ] No changes outside Scope
