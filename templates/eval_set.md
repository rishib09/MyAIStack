# Eval set format (JSONL)

One line is one workflow test. Every line is one JSON object.

## Fields

| Field | Required | Type | Meaning |
|---|---|---|---|
| `id` | yes | string | Workflow test ID, for example `WT1`. Must match a row in the workflow file. |
| `workflow` | yes | string | Workflow ID, for example `W-001`. |
| `risk_area` | yes | string | The risk area this test covers. Must match the workflow's "Risk areas" table. |
| `intent` | yes | string | `functional` or `adversarial`. |
| `kind` | yes | string | `single-turn` or `multi-turn`. |
| `input` | yes | string or list | A single-turn test: one string. A multi-turn test: a list of user turns, in order. |
| `pass_condition` | yes | string | The testable condition, in words. |
| `metric` | yes | string | The metric name, for example `recall`, `filter_compliance`, `hallucination_rate`. |
| `threshold` | yes | string | The pass threshold, for example `>= 0.8` or `= 0`. |
| `expected` | no | object | Machine-checkable expectations, for example `{"titles_exact": [...]}` or `{"max_runtime": 90}`. |

## Template line

```json
{"id": "WT1", "workflow": "W-001", "risk_area": "<risk area>", "intent": "functional", "kind": "single-turn", "input": "<prompt>", "pass_condition": "<condition>", "metric": "<metric>", "threshold": "<threshold>", "expected": {}}
```

## Multi-turn template line

```json
{"id": "WT2", "workflow": "W-002", "risk_area": "<risk area>", "intent": "functional", "kind": "multi-turn", "input": ["<turn 1>", "<turn 2>"], "pass_condition": "<condition on the final reply>", "metric": "<metric>", "threshold": "<threshold>", "expected": {}}
```

## Rules

- Do not edit or delete a line after the user confirms the workflow tests. Add new lines only.
