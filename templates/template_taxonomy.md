# Coding Work Taxonomy: Templates v0.2

## Rules at a glance

```
Project Map ──► Intent ──► filed as one of: Feature | Workflow | Work item (task | bug)

Feature ──► Workflow ──► Work item
   │                        │
   └──► Modules ◄───────────┘  every work item is tagged to one module
```

| Level | What it is |
|---|---|
| **Project Map** | A repo or sub-project under a repo. It is either greenfield or brownfield. This is where you write the project description and the setup commands an agent needs before working. |
| **Module** | A directory or subsystem, for example auth, storage, UI. Work is delivered through features and work items, never as a module by itself. |
| **Intent** | A raw user request. The agent restates it as a functional requirement, then files it as a **Feature**, **Workflow**, or **Work item**. The user approves the filing. The intent is recorded in a `Source intent` block at the top of the item it was filed as. It has no file of its own. |
| **Feature** | "User can X". It is the demoable unit and spans one or more modules. |
| **Workflow** | One scenario through a feature: an input, a sequence of steps and an outcome. A feature can have multiple workflows, one per scenario. Alternative designs for the same scenario are rows in the workflow's `Design options` table, not separate workflows. The workflow file records the chosen design pattern, with examples of frameworks or libraries that apply the project's coding standards. |
| **Work item** | **One PR.** It has a type of task or bug. This is where the work is broken down: exact to-do items, the tests to write and their type, and data structures or algorithms where the choice is not obvious. |

- **Bug test:** a bug only exists if a written acceptance criterion or contract is broken. If none is broken, the item is a new requirement and should be filed as a task.
- **Contract:** a documented input/output promise: API shape, function signature, or error behavior.
- **IDs:** `P-001` Project Map, `M-001` Module, `F-001` Feature, `W-001` Workflow, `T-001` task, `B-001` bug. Design options are numbered `D-A`, `D-B` within their workflow. Workflow tests are numbered `WTn` within their workflow. Component tests are numbered `CTn` within their work item.
- **Status:** every item uses the values in the Status table below.
- **Sizing guide for one PR:** a single module, a single concern. If an item needs "and" in its title, split it.
- **Modules:** they live as a table inside the Project Map file, not as separate files.
- **Design options:** exactly one option is `chosen`. A rejected option is one table row with an ID, a one-line design, its status and the reason. It never gets steps, libraries, risk areas or tests.
- **Storage:** all items are markdown files in the repo by default. Export them one-way to GitHub Issues only when the user asks. The repo stays the source of truth, and issue titles keep the same ID, for example `[T-001] Add intent router node`.

**Status**

| Status | Meaning | Applies to |
|---|---|---|
| `draft` | Being written. Not yet approved by the user. | All |
| `ready` | Approved by the user and can be started. For a workflow, the user approved the chosen design and confirmed the workflow tests. | All |
| `in-progress` | Work has started. | All |
| `in-review` | The PR is open and waiting for review. | Work item only |
| `done` | Acceptance criteria are met. For the project, the stage exit criteria are met. | All |
| `dropped` | Removed from scope. Keep the file and write the reason in it. | All |

**Testing rules**

| | Workflow tests (WT) | Component tests (CT) |
|---|---|---|
| View | Black-box: goes through the public interface (UI, API, CLI) and checks outcomes | White-box: checks one component of the code |
| Derived from | Risk areas, which are the weaknesses of the chosen design | The workflow tests they protect |
| Metrics | Outcome: answer recall and precision, ordering, faithfulness, refusal correctness | Component: router accuracy, recall@k, null handling, latency |
| Confirmed by | **The user, once per workflow (a gate)** | Generated from the workflow tests. Flagged to the user when a component test contradicts its workflow test |

- **Choosing the level.** Ask what question the test answers. "Can the user try out X as described?" is asked at the workflow level, so it is a workflow test. "Does this one component behave correctly?" is asked at the work-item level, so it is a component test.
- **Unit vs component.** A unit test is a component test at the unit level (tests one function or class). "Component test" is the umbrella term in these templates.
- **Traceability.** Every component test carries `Protects: W-xxx/WTn` or a contract line. A component test that protects nothing is either unnecessary or a sign that a workflow test is missing.
- **Confirmed tests are frozen.** After the user confirms a workflow's tests, agents do not edit or delete them. Agents may add new tests.
- **Count is driven by risk, not by a fixed number.**
  - Workflow: at least one test per risk area. High-severity risk areas (wrong output reaches the user silently, or money, data or security is read, written, or exposed) get several tests.
  - Work item: at least one component test for each workflow test or contract line the item touches. A small task may need one test. A core component may need many.
- **Adversarial by default.** Every risk area that can be attacked or misled (ambiguous input, injection, missing data, impossible requests) gets at least one adversarial workflow test, and every work item gets at least one adversarial component test. Dropping adversarial tests requires a written waiver from the user, recorded in the workflow or work item.

**Test axes:** a test may also be described by level (unit, integration, e2e/live, eval), interface (UI, backend/API, CLI), mode (automated, manual) and intent (functional, adversarial). These are vocabulary, not required tags.

**Greenfield vs brownfield**

- **Greenfield:** plan top-down, in the order Project Map, then Modules, then Features, then Workflows, then Work items.
- **Brownfield:** record existing modules and workflows *before* adding anything new. Ask the user to create a codebase knowledge graph that agents can use, and link it in the Project Map. New features attach to existing workflows. Create a new workflow only when none fits. Every work item states the files and modules it may affect and lists what it must not touch.
