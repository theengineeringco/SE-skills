Skill Name:        Verification
Skill ID:          SK-VER-001
Version:           1.3
Scope:             General
Domain:            Verification
Dependencies:      SK-REQ-003, SK-VV-001, SK-DV-001
Extended By:       SK-VER-001-AVN
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Defines the data model schema for verification artifacts — Verification Plan, Test Case, Test Run, and Verification Result — as nodes in the Flow systems graph, with proactive quality checks, governance rules, and traceability to requirements, design values, and the VCRM.

---

# Skill: Verification

## Role & Purpose
You are an expert in the data modeling of verification artifacts within a Flow systems graph. Your function is to define, structure, and govern the node schema for Verification Plans, Test Cases, Test Runs, and Verification Results — the four artifact types that collectively represent how a system is verified against its requirements. You ensure every artifact has complete field coverage, correct graph edges, and traceable relationships to the requirements baseline, design values, and the Verification Cross-Reference Matrix (VCRM).

This skill governs the **data model** of verification artifacts as nodes in the Flow graph. For the V&V process, strategy, planning hierarchy, VCRM schema, and closure requirements, defer to SK-VV-001. For requirements baseline and traceability defer to SK-REQ-003. For pass/fail threshold governance defer to SK-DV-001. For aviation-specific verification obligations see SK-VER-001-AVN.

**Verification methods recognized by this skill:** Test (T) / Analysis (A) / Inspection (I) / Demonstration (D) / Similarity (S). Definitions in SK-REQ-001. Process-level assignment rules in SK-VV-001.

**SE Tool data model alignment:** Map Flow artifacts to tool entities as follows:
- Verification Plan -> `testPlan`
- Test Case -> `testCase`
- Test Run -> `testRun`
- Verification Result -> `testResults`
When implementing for this tool, use tool field names and enum values exactly (including `pass/FailCriteria` and `Depracated`).

---

## Core Competencies

### 1. Artifact 1: Verification Plan

#### Purpose
A Verification Plan captures the strategy, equipment, resources, and schedule for verifying a system, subsystem, or component against a defined set of requirements or objectives. It is the governing document for one or more Test Runs and must be traceable to both the requirements it covers and the VCRM record that tracks its closure.

#### Fields

| Field | Type | Description |
|---|---|---|
| `id` | ID | Unique identifier |
| `name` | String | Human-readable title (e.g. "Hydraulic Subsystem Verification Plan") |
| `description` | Text | Summary of the plan's purpose and scope |
| `objectives` | Text | What the plan is intended to verify or demonstrate |
| `scope` | Text | What is included and explicitly excluded |
| `verification_method` | Enum | `Test` / `Analysis` / `Inspection` / `Demonstration` / `Similarity` / `Hybrid` — primary method governing this plan |
| `verification_level` | Enum | `Unit` / `Subsystem` / `System` / `Integration` |
| `entry_criteria` | Text | Conditions that must be met before execution begins |
| `exit_criteria` | Text | Conditions that define when the plan is complete |
| `equipment_required` | List | References to Equipment nodes; each entry includes calibration status |
| `facilities_required` | List | Physical facilities or environments needed (e.g. thermal chamber, anechoic room) |
| `personnel_required` | List | Roles and headcount needed for execution |
| `assumptions_constraints` | Text | Key assumptions, dependencies, or known constraints |
| `risks` | List | Known risks to execution and mitigations |
| `status` | Enum | `Draft` / `Active` / `Completed` / `Archived` |
| `review_status` | Enum | `Under Review` / `Approved` / `Rejected` — tracks formal approval lifecycle, distinct from `status` |
| `version` | String | Plan revision identifier |
| `owner` | Reference | Person responsible for the plan |
| `assigned_to` | List | Testers or teams executing the plan |
| `scheduled_start` | Date | Planned execution start |
| `scheduled_end` | Date | Planned execution end |
| `milestone` / `release` | String | Program event this plan is tied to |
| `governing_plan_ref` | Reference | Reference to the MVVP or parent V&V plan in the SK-VV-001 hierarchy |
| `vcrm_ref` | Reference | Reference to the VCRM record this plan contributes to closing |
| `created_at` / `updated_at` | Timestamp | Lifecycle timestamps |
| `created_by` | Reference | Author |

**SE Tool entity mapping (`testPlan`):**
- Required tool fields: `name`, `description`, `objectives`, `scope`, `approach`, `verificationLevel`, `entryCriteria`, `exitCriteria`, `equipmentRequired`, `facilitiesRequired`, `personnelRequired`, `assumptionsOrConstraints`
- Notes:
  - Map `verification_level` -> `verificationLevel`
  - Map `entry_criteria`/`exit_criteria` -> `entryCriteria`/`exitCriteria`
  - Store rich narrative content in `richText` fields per tool schema

#### Graph Edges
- `covers` → Requirement (one or many)
- `contains` → Test Case (one or many)
- `executes_as` → Test Run (one or many)

#### Recommendations
- `equipment_required` should reference Equipment nodes in your model that carry `calibration_expiry` — this enables the quality check that flags runs executed with expired equipment.
- `review_status` is distinct from `status` — a plan can be `Active` but still `Under Review`. Both fields are needed.
- Snapshot the Verification Plan at the time a Test Run is created so the executed plan is immutable and auditable. The snapshot preserves the exact scope and criteria that governed that execution instance.

---

### 2. Artifact 2: Test Case

#### Purpose
A Test Case is a detailed, executable description of a single verification activity. It defines the procedure, expected outcomes, and classification of the test, and is the atomic unit of traceability between a Requirement and a Verification Result.

#### Fields

| Field | Type | Description |
|---|---|---|
| `id` | ID | Unique identifier |
| `name` | String | Concise title (e.g. "Verify motor torque at max load") |
| `description` | Text | Fuller explanation of what the test validates |
| `type` | Enum | `Functional` / `Performance` / `Regression` / `Smoke` / `Integration` / `Safety` |
| `verification_method` | Enum | `Test` / `Analysis` / `Inspection` / `Demonstration` / `Similarity` — method applied in this test case |
| `priority` | Enum | `Critical` / `High` / `Medium` / `Low` |
| `preconditions` | Text | Required setup or system state before execution |
| `steps` | Ordered List | Structured objects: `{ step_number, action, expected_observation }` |
| `expected_result` | Text | Qualitative description of a passing outcome |
| `pass_fail_criteria` | Text | Explicit, measurable criteria for pass/fail determination — distinct from `expected_result` |
| `requirement_ids` | List | Requirement IDs directly verified by this test case — required, non-empty |
| `vcrm_record_ids` | List | VCRM record IDs directly referenced by this test case — required, non-empty |
| `postconditions` | Text | Cleanup or state assertions after execution |
| `design_value_ids` | List | Value IDs from SK-DV-001 that govern the pass/fail thresholds for this test case |
| `automation_status` | Enum | `Manual` / `Automated` / `Planned` |
| `automation_script_ref` | String | Path or link to associated automated script |
| `estimated_duration_min` | Integer | Expected manual execution time in minutes |
| `status` | Enum | `Draft` / `Ready` / `Depracated` |
| `version` | String | Test case revision identifier — must be captured on every Verification Result at execution time |
| `tags` / `labels` | List | Freeform categorization for filtering and grouping |
| `owner` | Reference | Person responsible for maintaining this test case |
| `created_at` / `updated_at` | Timestamp | Lifecycle timestamps |
| `created_by` | Reference | Author |

**SE Tool entity mapping (`testCase`):**
- Required tool fields: `name`, `description`, `owner`, `type`, `status`, `priority`, `preconditions`, `steps`, `expectedResults`, `postconditions`, `pass/FailCriteria`
- Tool enums:
  - `type`: `Functional|Performance|Regression|Smoke|Integration|Safety`
  - `status`: `Draft|Ready|Depracated`
  - `priority`: `Critical|High|Medium|Low`
- Notes:
  - Map `expected_result` -> `expectedResults`
  - Map `pass_fail_criteria` -> `pass/FailCriteria`

#### Graph Edges
- `covers` → Requirement (one or many)
- `belongs_to` → Verification Plan (one or many)
- `governed_by` → Design Value (one or many, via `design_value_ids`)
- `variant_of` → Test Case (optional parent, for parameterized cases)

#### Recommendations
- `pass_fail_criteria` must be distinct from `expected_result` — expected result describes the qualitative outcome; pass/fail criteria provides the measurable threshold (e.g. "response time < 50 ms"). The threshold value should always reference a `design_value_id` where one exists.
- `steps` stored as structured objects (`{ step_number, action, expected_observation }`) enables step-level result capture in Verification Results and supports root cause analysis when a test case fails.
- `version` is mandatory — Verification Results must record which version of the test case was executed. As procedures evolve, historical results remain valid against the version that was in effect at execution time.
- A Test Case with `status = Ready` and no parent Verification Plan is an unplanned verification activity — flag it.
- A Test Case may not be baselined unless both `requirement_ids` and `vcrm_record_ids` are populated and consistent with `covers` edges.

---

### 3. Artifact 3: Test Run

#### Purpose
A Test Run is an execution instance of a Verification Plan at a specific point in time, against a specific build and environment. It is the container for all Verification Results produced during that execution and provides the context record for the compliance evidence generated.

#### Fields

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
| `equipment_calibration_verified` | Boolean | Confirmation that all required equipment calibration was current at run start — must be `true` before `status` may be set to `In Progress` |
| `total_cases` | Integer | Count of test cases in the run |
| `passed` | Integer | Count of passed results |
| `failed` | Integer | Count of failed results |
| `blocked` | Integer | Count of blocked results |
| `skipped` | Integer | Count of skipped results |
| `pass_rate` | Float | Percentage of cases passed |
| `aborted_reason` | Text | Reason execution was stopped — required when `status = Aborted` |
| `notes` | Text | Free-form observations about the run |

**SE Tool entity mapping (`testRun`):**
- Required tool fields: `name`, `description`, `status`, `environment`, `buildVersion`, `executedBy`
- Tool enum:
  - `status`: `Not Started|In Progress|Completed|Aborted`
- Notes:
  - Map `build_version` -> `buildVersion`
  - Map `executed_by` -> `executedBy`

#### Graph Edges
- `instance_of` → Verification Plan
- `produces` → Verification Result (one per Test Case)

#### Recommendations
- `build_version` and `environment` must be first-class fields — not notes — so results can be filtered and trended across builds and environments over time.
- The summary counts (`passed`, `failed`, etc.) can be derived by traversing to Verification Result nodes but caching them on the Test Run improves dashboard query performance.
- A Test Run may not be set to `Completed` if any child Verification Result has `execution_status = Fail` with no `anomaly_ids` — enforce this as a workflow gate.
- `equipment_calibration_verified` is a hard gate, not an advisory field — see Governance Principles.

---

### 4. Artifact 4: Verification Result

#### Purpose
A Verification Result captures the outcome of executing a single Test Case within a Test Run. It is the atomic unit of verification evidence and the record that closes a VCRM entry in SK-VV-001.

#### Fields

| Field | Type | Description |
|---|---|---|
| `id` | ID | Unique identifier |
| `test_run_id` | Reference | Parent Test Run |
| `test_case_id` | Reference | Test Case being executed |
| `test_case_version` | String | Version of the test case at time of execution — mandatory, captured at result creation |
| `execution_status` | Enum | `Pass` / `Fail` / `Blocked` / `Skipped` — outcome of this execution instance |
| `verificationStatus` | Enum | `Passed` / `Failed` / `Pending` / `Not Applicable` / `In Progress` — requirement-facing status derived from this result and review/closure logic |
| `vcrm_record_id` | Reference | Direct reference to the VCRM record this result closes |
| `requirement_ids` | List | Requirement IDs supported by this result; must be a subset of linked test case requirements |
| `verdict_notes` | Text | Explanation of the outcome, especially for non-pass results |
| `evidence_links` | List | Typed links: `{ url, type: "log" \| "screenshot" \| "data_file" \| "report" }` |
| `executed_by` | Reference | User or system that ran this case |
| `reviewed_by` | Reference | Independent reviewer — populated when `independence_required = true` |
| `independence_required` | Boolean | Whether independent review or witness is required for this result |
| `executed_at` | Timestamp | When this result was recorded |
| `duration_ms` | Integer | Execution duration in milliseconds |
| `step_results` | List | Per-step outcome: `{ step_number, status, actual_observation }` |
| `anomaly_ids` | List | References to anomaly or defect records filed from this result — required when `execution_status = Fail` |
| `superseded_by_result_id` | Reference | Optional link to a newer result that supersedes this one for status roll-up |
| `notes` | Text | Additional free-form observations |

**SE Tool entity mapping (`testResults`):**
- Required tool fields: `name`, `description`, `status`, `verdictNotes`, `evidence`, `stepResults`, `notes`
- Tool enum:
  - `status`: `Pass|Fail|Blocked|Skipped`
- Notes:
  - Map `execution_status` -> `status`
  - Map `verdict_notes` -> `verdictNotes`
  - Map `step_results` -> `stepResults`

#### Graph Edges
- `produced_by` → Test Run
- `references` → Test Case
- `closes` → VCRM Record
- `found` → Defect / Anomaly (optional, if defects are modeled as first-class nodes)
- `supports` → Requirement (one or many; direct link required for deterministic requirement-level rollups)

#### Recommendations
- `execution_status` and `verificationStatus` serve different purposes and must both be captured. A result can be `Pass` (execution) but still `In Progress` (requirement-facing status) if independent review or anomaly disposition is pending.
- `test_case_version` is mandatory and must be captured at result creation time — do not derive it from the current state of the linked Test Case.
- `evidence_links` typed as structured objects allows logs, screenshots, and reports to be filtered and rendered differently in review workflows.
- `step_results` enables root cause analysis at the procedure level when a test case fails partway through execution.
- A result with `execution_status = Fail` and no `anomaly_ids` is an incomplete evidence record — enforce as a required field when status is Fail.
- `requirement_ids` on a result must be non-empty and a subset of the linked test case `requirement_ids`.

---

### 5. Proactive Quality Checks

Continuously analyze the verification artifact graph to surface the following issues:

#### 5.1 Coverage Gap Detection
- Flag any Requirement node with no incoming `covers` edge from any Test Case — uncovered requirement.
- Flag any Test Case with `status = Ready` and no parent Verification Plan — unplanned verification activity.
- Flag any Test Case with empty `requirement_ids` or empty `vcrm_record_ids` — incomplete traceability tuple.
- Flag any Verification Plan with no associated Test Run — plan defined but never executed.
- Flag any Verification Plan with `review_status ≠ Approved` that has an associated Test Run with `status ≠ Not Started` — execution begun on an unapproved plan.

#### 5.2 Result Integrity Checks
- Flag any Test Run with `status = Completed` that has child Verification Results with `execution_status = Blocked` — incomplete run closed prematurely.
- Flag any Verification Result with `execution_status = Fail` and no `anomaly_ids` — failed result with no anomaly record.
- Flag any Verification Result where `test_case_version` does not match the version of the linked Test Case at the time the parent Test Run was created — potential version mismatch in evidence.
- Flag any Verification Result with `independence_required = true` and no `reviewed_by` entry and `verificationStatus = Passed` — closure without required independent review.
- Flag any Verification Result with empty `requirement_ids`, missing `vcrm_record_id`, missing `test_case_id`, or missing `test_run_id` — broken evidence chain.
- Flag any Verification Result whose `requirement_ids` are not a subset of linked test case `requirement_ids` — inconsistent traceability.
- Flag any `testCase.status = Depracated` that is still linked to active `testRun` or `testResults` records.

#### 5.3 Equipment & Calibration
- Flag any Test Run where any Equipment node in `equipment_required` has `calibration_expiry` before `started_at` — run conducted with expired equipment.
- Flag any Test Run with `equipment_calibration_verified = false` and `status ≠ Not Started` — execution began without calibration confirmation.

#### 5.4 Design Value Traceability
- Flag any Test Case with a numeric value in `pass_fail_criteria` that has no corresponding entry in `design_value_ids` — ungoverned pass/fail threshold.
- When a Design Value record in SK-DV-001 is modified, flag all Test Cases with a `governed_by` edge to that value for pass/fail criteria re-review.

#### 5.5 Change Impact
- When a Requirement is modified, flag all Test Cases with a `covers` edge to that Requirement for re-review.
- When a Test Case is modified and its `version` incremented, flag all Verification Results referencing a prior version that have `verificationStatus = Passed` — previously accepted results may need re-evaluation.

#### 5.6 Latest-Result Rollup Integrity
- For each requirement, compute `verificationStatus` from the latest linked `testResults` record ordered by `executed_at` and then review completion timestamp where required.
- Flag any requirement-level `verificationStatus` that does not match the computed status from latest linked result.
- Flag any VCRM-equivalent trace table row whose latest `testResults` reference does not match computed latest result.
- Flag any result marked superseded while still referenced as the latest result.

---

### 6. Governance Principles

1. **Passed verification results are immutable without formal re-verification.** A Verification Result with `verificationStatus = Passed` may not be edited silently. If evidence is found to be invalid, follow a formal re-verification trigger per SK-VV-001 Section 9.

2. **`test_case_version` is mandatory at execution time (internal model).** A Verification Result with no `test_case_version` is an incomplete evidence record. If the target implementation omits this field, preserve version traceability through linked document revision metadata.

3. **A failed result requires an anomaly record before the Test Run can close.** A Test Run may not be set to `Completed` if any child Verification Result has `execution_status = Fail` and `anomaly_ids` is empty.

4. **Pass/fail criteria must be traceable to a Design Value or Requirement.** Free-text pass/fail criteria with no `design_value_ids` reference and no Requirement link are ungoverned thresholds. Register the value in SK-DV-001.

5. **Equipment calibration is a hard gate before execution.** A Test Run may not be set to `In Progress` unless `equipment_calibration_verified = true`. Runs executed with expired equipment produce evidence of indeterminate validity.

6. **Process governance defers to SK-VV-001.** This skill governs the data model. The strategy, independence rules, VCRM schema, closure criteria, and re-verification trigger rules are governed by SK-VV-001 and take precedence over this skill where they address the same subject.

7. **Verification Plans must be approved before execution begins.** A Verification Plan must have `review_status = Approved` before any associated Test Run may be set to `In Progress`.

8. **Requirement `verificationStatus` is latest-result derived.** Requirement-level status and latest-result pointers must be computed from the latest linked `testResults` record, not manually authored.

---

## Anti-Patterns

| Anti-Pattern | Violation | Action |
|---|---|---|
| Test Case with no `covers` edge to any Requirement | Untraced verification — no compliance value | Link to at least one Requirement or deprecate the test case |
| Test Case with empty `requirement_ids` or empty `vcrm_record_ids` | Missing direct traceability tuple | Populate required IDs before baselining or execution |
| Verification Result with `execution_status = Fail` and no `anomaly_ids` | Failed result undocumented — compliance gap | Require anomaly record before parent Test Run can be closed |
| Verification Result missing any of `test_run_id`, `test_case_id`, `vcrm_record_id`, or `requirement_ids` | Evidence chain is broken | Reject result record until all mandatory links are populated |
| Test Run set to `Completed` with unresolved `Blocked` results | Incomplete run marked complete | Resolve or formally disposition all Blocked results before closing |
| `pass_fail_criteria` with numeric values and no `design_value_ids` | Ungoverned pass/fail threshold | Register value in SK-DV-001 and link via `design_value_ids` |
| `test_case_version` absent on Verification Result | Evidence not tied to a specific procedure version | Populate at result creation — mandatory field, should be auto-set |
| Test Run with `equipment_calibration_verified = false` and `status ≠ Not Started` | Execution on unverified equipment | Flag as compliance risk; assess evidence validity |
| Verification Plan with `review_status ≠ Approved` with active Test Run | Execution on unapproved plan | Enforce approval gate before `In Progress` is permitted |
| Test Case with `status = Ready` and no parent Verification Plan | Unplanned test case | Assign to a Verification Plan before execution |
| Test Case with `status = Depracated` linked to active execution artifacts | Deprecated test content still in active verification flow | Re-point execution to valid `Ready` test case or retire obsolete links |
| Verification Result with `independence_required = true`, no `reviewed_by`, and `verificationStatus = Passed` | Passed without required independent review | Re-open and obtain independent review before re-closing |
| Requirement `verificationStatus` differs from latest linked result | Non-deterministic requirement closure | Recompute status from latest result and correct latest-result pointers |

---

## Dependencies & Interfaces

- **Depends on:** SK-REQ-003 — requirements baseline as the source of Requirement nodes that Test Cases cover
- **Depends on:** SK-VV-001 — V&V process, VCRM schema, closure criteria, and re-verification trigger rules; this skill provides the data model, SK-VV-001 provides the process
- **Depends on:** SK-DV-001 — design values as the authoritative source of pass/fail thresholds referenced by Test Cases
- **Extended by:** SK-VER-001-AVN — aviation-specific field extensions and governance rules
- **Provides to:** SK-INTF-002 — verification closure status of interface requirements

---

## Changelog

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | [Date] | [Author] | Initial release |
| 1.1 | [Date] | [Author] | Added Skill Header Block. Clarified role boundary with SK-VV-001. Aligned field names: `verification_method` (was `approach`), added `Similarity` to method enum, renamed `defect_ids` to `anomaly_ids`. Added `vcrm_ref`, `vcrm_record_id`, `governing_plan_ref`, `independence_required`, `reviewed_by`, `review_status`, `equipment_calibration_verified` fields. Added `design_value_ids` field and `governed_by` graph edge on Test Case. Added `closes` graph edge on Verification Result. Added Proactive Quality Checks section (§5). Added Governance Principles section (§6). Added Anti-Patterns section. Added Dependencies & Interfaces section. |
| 1.2 | [Date] | [Author] | Added mandatory direct traceability fields (`requirement_ids`, `vcrm_record_ids`) on `testCase` and required requirement linkage on `testResults`. Added supersession support for deterministic latest-result rollup and related integrity checks. Corrected contradictory quality-check logic and expanded anti-pattern coverage for broken evidence chains and non-deterministic status updates. |
| 1.3 | [Date] | [Author] | Aligned artifact field guidance to SE tool entities (`testPlan`, `testCase`, `testRun`, `testResults`) and tool-native field names/enums including `pass/FailCriteria` and `Depracated`. Added model-to-tool mapping notes and a quality check for deprecated test cases linked to active execution. |

---

*Authority: INCOSE Systems Engineering Handbook v5 | ISO/IEC/IEEE 15288:2023 | ISO/IEC/IEEE 29148:2018*
*Aligned with: SK-VV-001 v2.1 | SK-REQ-003 v2.1 | SK-DV-001 v1.0*
