# Verification Skill

## Overview
This skill guides the creation of verification artifacts within a systems model. It supports any level of system hierarchy and any verification objective, from unit-level functional tests to system-level qualification campaigns.

---

## Artifact 1: Verification Plan

### Purpose
A Verification Plan captures the strategy, equipment, resources, and schedule for verifying a system, subsystem, or component against a defined set of requirements or objectives.

### Fields

| Field | Type | Description |
|---|---|---|
| `id` | ID | Unique identifier |
| `name` | String | Human-readable title (e.g. "Hydraulic Subsystem Verification Plan") |
| `description` | Text | Summary of the plan's purpose and scope |
| `objectives` | Text | What the plan is intended to verify or demonstrate |
| `scope` | Text | What is included and explicitly excluded |
| `approach` | Enum | `Analysis` / `Test` / `Inspection` / `Demonstration` / `Hybrid` |
| `verification_level` | Enum | `Unit` / `Subsystem` / `System` / `Integration` |
| `entry_criteria` | Text | Conditions that must be met before execution begins |
| `exit_criteria` | Text | Conditions that define when the plan is complete |
| `equipment_required` | List | Test equipment, tooling, fixtures, or lab resources needed |
| `facilities_required` | List | Physical facilities or environments needed (e.g. thermal chamber, anechoic room) |
| `personnel_required` | List | Roles and headcount needed for execution |
| `assumptions_constraints` | Text | Key assumptions, dependencies, or known constraints |
| `risks` | List | Known risks to execution and mitigations |
| `status` | Enum | `Draft` / `Active` / `Completed` / `Archived` |
| `version` | String | Plan revision identifier |
| `owner` | Reference | Person responsible for the plan |
| `assigned_to` | List | Testers or teams executing the plan |
| `scheduled_start` | Date | Planned execution start |
| `scheduled_end` | Date | Planned execution end |
| `milestone` / `release` | String | Program event this plan is tied to |
| `created_at` / `updated_at` | Timestamp | Lifecycle timestamps |
| `created_by` | Reference | Author |

### Graph Edges
- `covers` → Requirement (one or many)
- `contains` → Test Case (one or many)
- `executes_as` → Test Run (one or many)

### Recommendations
- Capture `verification_method` at the plan level to distinguish test campaigns from analysis or inspection activities — this matters for traceability and compliance reporting.
- `equipment_required` should reference equipment nodes in your model if you track calibration status, so you can flag when a plan's required equipment is out of calibration.
- Consider a `review_status` field (`Under Review` / `Approved` / `Rejected`) distinct from `status` to track the formal approval lifecycle of the plan document.

---

## Artifact 2: Test Case

### Purpose
A Test Case is a detailed, executable description of a single verification activity. It defines the procedure, expected outcomes, and classification of the test.

### Fields

| Field | Type | Description |
|---|---|---|
| `id` | ID | Unique identifier |
| `name` | String | Concise title (e.g. "Verify motor torque at max load") |
| `description` | Text | Fuller explanation of what the test validates |
| `type` | Enum | `Functional` / `Performance` / `Regression` / `Smoke` / `Integration` / `Safety` |
| `priority` | Enum | `Critical` / `High` / `Medium` / `Low` |
| `preconditions` | Text | Required setup or system state before execution |
| `steps` | Ordered List | Step-by-step procedure actions |
| `expected_result` | Text | What a passing outcome looks like |
| `postconditions` | Text | Cleanup or state assertions after execution |
| `pass_fail_criteria` | Text | Explicit, measurable criteria for pass/fail determination |
| `automation_status` | Enum | `Manual` / `Automated` / `Planned` |
| `automation_script_ref` | String | Path or link to associated automated script |
| `estimated_duration_min` | Integer | Expected manual execution time in minutes |
| `status` | Enum | `Draft` / `Ready` / `Deprecated` |
| `version` | String | Test case revision identifier |
| `tags` / `labels` | List | Freeform categorization |
| `owner` | Reference | Person responsible for maintaining this test case |
| `created_at` / `updated_at` | Timestamp | Lifecycle timestamps |
| `created_by` | Reference | Author |

### Graph Edges
- `covers` → Requirement (one or many)
- `belongs_to` → Verification Plan (one or many)
- `variant_of` → Test Case (optional parent, for parameterized cases)

### Recommendations
- `pass_fail_criteria` should be distinct from `expected_result` — expected result describes the qualitative outcome, while pass/fail criteria provides the measurable threshold (e.g. "response time < 50ms").
- Store `steps` as structured objects (`{ step_number, action, expected_observation }`) rather than plain text so results can be captured at the step level.
- `version` is critical — Test Results should record which version of a test case was executed to preserve historical integrity as procedures evolve.

---

## Artifact 3: Test Run

### Purpose
A Test Run is an execution instance of a Verification Plan at a specific point in time, against a specific build and environment. It serves as the container for all results produced during that execution.

### Fields

| Field | Type | Description |
|---|---|---|
| `id` | ID | Unique identifier |
| `name` | String | Human-readable label (e.g. "Sprint 14 Regression — HW Rev B") |
| `verification_plan_id` | Reference | Parent Verification Plan |
| `status` | Enum | `Not Started` / `In Progress` / `Completed` / `Aborted` |
| `environment` | String | Where the test was executed (e.g. "Staging", "Lab Bench 3", "Hardware Rev B") |
| `build_version` | String | Software or hardware version under test |
| `commit_sha` | String | Source control reference (if applicable) |
| `executed_by` | Reference | User or system that triggered the run |
| `started_at` | Timestamp | When execution began |
| `completed_at` | Timestamp | When execution finished |
| `created_at` | Timestamp | When the run was created |
| `total_cases` | Integer | Count of test cases in the run |
| `passed` | Integer | Count of passed results |
| `failed` | Integer | Count of failed results |
| `blocked` | Integer | Count of blocked results |
| `skipped` | Integer | Count of skipped results |
| `pass_rate` | Float | Percentage of cases passed |
| `aborted_reason` | Text | Reason execution was stopped (populated when status = Aborted) |
| `notes` | Text | Free-form observations about the run |

### Graph Edges
- `instance_of` → Verification Plan
- `produces` → Verification Result (one per Test Case)

### Recommendations
- Store `build_version` and `environment` as first-class fields so you can filter and trend results across builds and environments over time.
- The summary counts (`passed`, `failed`, etc.) can be derived by traversing to Verification Result nodes, but caching them on the Test Run improves dashboard query performance.

---

## Artifact 4: Verification Result

### Purpose
A Verification Result captures the outcome of executing a single Test Case within a Test Run. It is the atomic unit of verification evidence.

### Fields

| Field | Type | Description |
|---|---|---|
| `id` | ID | Unique identifier |
| `test_run_id` | Reference | Parent Test Run |
| `test_case_id` | Reference | Test Case being executed |
| `test_case_version` | String | Version of the test case at time of execution |
| `status` | Enum | `Pass` / `Fail` / `Blocked` / `Skipped` |
| `verdict_notes` | Text | Explanation of the outcome, especially for non-pass results |
| `evidence_links` | List | Typed links to logs, screenshots, data files, test reports (`{ url, type }`) |
| `executed_by` | Reference | User or system that ran this case |
| `executed_at` | Timestamp | When this result was recorded |
| `duration_ms` | Integer | Execution duration in milliseconds |
| `step_results` | List | Per-step outcome (`{ step_number, status, actual_observation }`) |
| `defect_ids` | List | References to defects or issues filed from this result |
| `notes` | Text | Additional free-form observations |

### Graph Edges
- `produced_by` → Test Run
- `references` → Test Case
- `found` → Defect (optional, if defects are modeled as nodes)
- `supports` → Requirement (derived via Test Case, or direct for traceability)

### Recommendations
- `evidence_links` should be typed (`{ url, type: "log" | "screenshot" | "data_file" | "report" }`) so evidence can be filtered and rendered appropriately in review workflows.
- `test_case_version` should always be captured at result creation time — do not rely on the current version of the linked Test Case.
- `step_results` as structured objects enables root cause analysis at the procedure level.

---

## Cross-Cutting Recommendations

- **Coverage Gap Detection** — query the graph for Requirements with no incoming `covers` edge to find uncovered requirements.
- **Defect Node** — model Defects as first-class nodes with edges from Verification Results, enabling traceability from a defect back to the requirement it violates.
- **Equipment Node** — model Equipment as nodes with `calibration_expiry` and reference them from Verification Plans to flag runs executed with expired equipment.
- **Approval / Signature Node** — for formal verification, capture reviewer approvals as a structured node or edge rather than a free-text field.
- **Baseline / Snapshot** — consider snapshotting a Verification Plan at the time a Test Run is created so the executed plan is immutable and auditable.
