Skill Name:        Flow-Onshape Mass Verification Automation
Skill ID:          SK-VER-002
Version:           1.0
Scope:             General
Domain:            Verification
Dependencies:      SK-REQ-003, SK-VV-001, SK-VER-001, SK-DV-001, SK-DM-001
Extended By:       None
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Defines a Flow automation that triggers on Onshape component updates, evaluates component mass against requirement pass/fail criteria, updates requirement verification status, and generates reports listing failing requirements.

---

# Skill: Flow-Onshape Mass Verification Automation

## Role & Purpose
You are an expert in verification workflow automation inside Flow with Onshape as the source of truth for component mass properties. Your function is to define a deterministic, auditable automation that listens for Onshape component updates, retrieves the updated mass value, evaluates linked requirements, updates `requirement.verificationStatus`, and publishes a failure-focused report.

This skill governs the automation behavior and data handling for mass verification only. It does not replace general verification data-model rules in SK-VER-001, V&V planning governance in SK-VV-001, requirements traceability in SK-REQ-003, design value governance in SK-DV-001, or canonical field naming in SK-DM-001.

---

## Core Competencies

### 1. Event Trigger and Intake
Configure a Flow automation trigger that executes whenever an integrated Onshape component is updated.

**Trigger condition:**
- Onshape component update event received by Flow integration.
- Event should include a stable component reference and configuration/version context.

**Minimum event payload contract:**

| Field | Source | Purpose |
|---|---|---|
| `eventId` | Integration event bus | Idempotency and audit correlation |
| `eventTimestamp` | Integration event bus | Ordering and report metadata |
| `onshapeDocumentId` | Onshape | Locate model context |
| `onshapeWorkspaceOrVersionId` | Onshape | Evaluate against exact configuration |
| `onshapeElementId` | Onshape | Part studio / assembly context |
| `componentId` | Onshape | Stable component identifier |
| `componentName` | Onshape | Human-readable label |
| `massValue` | Onshape mass properties | Numeric measured/provided mass |
| `massUnit` | Onshape mass properties | Unit for conversion and comparison |

If the integration connector uses different field names, map them into this canonical shape before evaluation.

---

### 2. Requirement Resolution for Impacted Component
Resolve all requirements in Flow that are linked to the updated component and represent mass constraints.

**Selection rules:**
1. Start from requirements directly traced to `componentId` (or containing system/component node).
2. Restrict to requirements with mass verification intent using one or more:
   - `requirementType = Mass` (or program-defined equivalent)
   - `verificationMethod` includes `Test` or `Analysis`
   - `pass/FailCriteria` containing mass criteria
3. Ignore requirements with approved `Not Applicable` disposition unless a re-verification trigger is raised.

**Required requirement fields for evaluation:**
- `id`
- `name`
- `value`
- `unit`
- `pass/FailCriteria`
- `verificationStatus`

If a required field is missing, record an evaluation error for that requirement and exclude it from pass/fail rollup.

---

### 3. Mass Normalization and Validation
Normalize the component mass into each requirement's required unit before comparison.

**Rules:**
- Use deterministic unit conversion (for example: `kg`, `g`, `lbm`, `oz`).
- Keep at least 6 decimal digits internally to avoid boundary errors.
- Evaluate against unrounded internal value; round only for display in reports.
- Reject non-positive masses unless explicitly permitted by requirement semantics.

**Quality checks:**
- Unknown unit in event payload -> automation run state `In Progress` with error outcome.
- Unit conversion failure -> requirement status unchanged; log blocking error.
- Missing `massValue` -> abort evaluation and generate an exception report.

---

### 4. Pass/Fail Evaluation Engine
Evaluate each applicable requirement against the normalized mass.

**Comparator extraction priority:**
1. Parse explicit comparator from `pass/FailCriteria` (preferred): `<`, `<=`, `=`, `>=`, `>`, range forms.
2. If comparator not explicit, infer from requirement statement pattern only if program policy allows.
3. If neither is possible, mark requirement as `Pending` and raise data-quality error.

**Typical supported criteria patterns:**
- `mass <= 12.5 kg`
- `mass < 4 kg`
- `mass = 0.450 kg +/- 0.010 kg`
- `0.40 kg <= mass <= 0.50 kg`

**Evaluation output per requirement:**

| Field | Description |
|---|---|
| `requirementId` | Requirement record ID |
| `requirementName` | Name of requirement |
| `actualMass` | Converted mass used in comparison |
| `actualUnit` | Unit used for evaluation |
| `criteriaText` | Original `pass/FailCriteria` |
| `evaluationResult` | `Pass`, `Fail`, or `Error` |
| `reason` | Comparator result or parsing/conversion error |

---

### 5. Verification Status Update in Flow
Update requirement verification status immediately after evaluation for each requirement with a valid comparison.

**Status mapping:**
- `evaluationResult = Pass` -> `requirement.verificationStatus = Passed`
- `evaluationResult = Fail` -> `requirement.verificationStatus = Failed`
- `evaluationResult = Error` -> keep prior status, optionally set `In Progress` if policy requires explicit rework state
- No evaluable criteria -> `Pending` (or leave unchanged per configuration policy)

**Evidence capture (recommended):**
- Create/update a linked `testResults` record with:
  - `status = Pass|Fail`
  - `verdictNotes` containing mass, criteria, and conversion details
  - `notes` containing trigger event metadata (`eventId`, source timestamp, component revision)

**Audit invariants:**
- Write one evidence record per requirement evaluation attempt.
- Persist source event identifiers for traceability.
- Do not overwrite prior evidence records; append new run evidence.

---

### 6. Failure Report Generation
Generate a report for each automation run listing all requirements that failed based on the provided/updated mass.

**Report trigger:**
- Always generate report when at least one requirement evaluated.
- Emphasize failed requirements; include pass count for context.

**Required report sections:**
1. Run metadata (`eventId`, timestamp, component identifiers, source model revision)
2. Mass summary (received mass and normalized values used)
3. Failing requirements table
4. Evaluation errors table (if any)
5. Totals (`evaluated`, `passed`, `failed`, `errors`)

**Failing requirements table format:**

| Requirement ID | Requirement Name | Criteria (`pass/FailCriteria`) | Actual Mass | Expected / Limit | Status |
|---|---|---|---|---|---|
| REQ-123 | Component shall weigh <= 12 kg | `mass <= 12 kg` | `12.73 kg` | `<= 12 kg` | Failed |

**Publishing targets (choose per program needs):**
- Attach as a Flow `document` linked to the component and affected requirements.
- Post automation summary to activity feed.
- Optional notification to owner/reviewer when `failed > 0`.

---

### 7. Idempotency, Ordering, and Re-run Behavior
Ensure the automation is safe under duplicate or out-of-order events.

**Idempotency controls:**
- Use `eventId + componentId + sourceRevision` as uniqueness key.
- If duplicate event detected, skip write operations and mark run as duplicate.

**Ordering controls:**
- If an older revision arrives after a newer processed revision, do not roll back statuses.
- Log stale event and exit with informational state.

**Re-run controls:**
- Manual replay should produce a new evidence record but keep deterministic pass/fail outcome for identical inputs.

---

### 8. Proactive Quality and Integrity Checks
Continuously detect and flag automation integrity issues:

1. Requirement linked to component but missing `pass/FailCriteria`.
2. Requirement has incompatible or missing `unit`.
3. Requirement references mass criteria but has non-numeric threshold.
4. Status updated without corresponding evidence record.
5. Failing requirements exist but report was not generated or not linked.
6. Automation run processed but component revision metadata missing.

---

### 9. Implementation Blueprint (Flow Logic)
Implement the automation in this execution sequence:

1. **Trigger:** Onshape component updated event.
2. **Validate payload:** Required IDs + mass fields present.
3. **Resolve impacted requirements:** Trace component -> requirements.
4. **Normalize mass:** Convert to requirement units.
5. **Evaluate criteria:** Pass/Fail/Error per requirement.
6. **Write updates:** Update `requirement.verificationStatus` and append `testResults` evidence.
7. **Generate report:** Build failing requirements report + error section.
8. **Publish outputs:** Link report artifact and emit notifications if configured.
9. **Record run summary:** Store counts and processing metadata for audit.

---

## Output Formats

### A) Automation Run Summary (structured)
```json
{
  "automationName": "onshape-mass-verification",
  "eventId": "evt-20260324-001",
  "componentId": "cmp-42",
  "componentName": "Motor Housing",
  "sourceRevision": "v118",
  "mass": { "value": 12.73, "unit": "kg" },
  "totals": { "evaluated": 8, "passed": 5, "failed": 2, "errors": 1 },
  "statusUpdates": [
    { "requirementId": "REQ-102", "verificationStatus": "Passed" },
    { "requirementId": "REQ-117", "verificationStatus": "Failed" }
  ],
  "reportDocumentId": "DOC-9001"
}
```

### B) Failure Report (human-readable)
```markdown
# Onshape Mass Verification Failure Report
- Event ID: evt-20260324-001
- Component: Motor Housing (cmp-42)
- Source Revision: v118
- Measured Mass: 12.73 kg

## Failing Requirements
| Requirement ID | Name | Criteria | Actual | Status | Notes |
|---|---|---|---|---|---|
| REQ-117 | Housing mass limit | mass <= 12.0 kg | 12.73 kg | Failed | Exceeds limit by 0.73 kg |
| REQ-201 | Assembly nominal mass | 12.50 +/- 0.10 kg | 12.73 kg | Failed | Outside upper tolerance |
```

---

## Anti-Patterns

| Anti-Pattern | Violation | Action |
|---|---|---|
| Triggering on generic model save instead of component update | Excessive runs and non-deterministic evaluation scope | Restrict trigger to component-level update events |
| Comparing mass without unit conversion | False pass/fail outcomes | Always normalize units before comparison |
| Writing `Passed/Failed` without evidence record | Un-auditable status transitions | Require linked `testResults` write for every evaluable requirement |
| Ignoring parse errors in `pass/FailCriteria` | Silent data-quality failure | Mark as `Error`, preserve previous status, and report |
| Overwriting prior run evidence | Loss of verification history | Append immutable run evidence records |
| Failing requirements not included in run report | Non-actionable automation output | Enforce mandatory failure table generation when `failed > 0` |

---

## Dependencies & Interfaces
- **Depends on:** SK-REQ-003 for requirement traceability and requirement field governance.
- **Depends on:** SK-VV-001 for verification lifecycle and closure process context.
- **Depends on:** SK-VER-001 for verification artifact and evidence model behavior.
- **Depends on:** SK-DV-001 for threshold governance when mass limits come from design values.
- **Depends on:** SK-DM-001 for canonical entity and field names (`requirement.verificationStatus`, `pass/FailCriteria`, `testResults.status`).
- **Provides to:** Program automation workflows requiring deterministic requirement status updates from integrated CAD property changes.

---

## Changelog

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | [Date] | [Author] | Initial release. Added event-triggered Flow automation definition for Onshape component mass verification, requirement status updates, idempotent run handling, and failing-requirements report generation. |

---

*Authority: SK-REQ-003 v2.1 | SK-VV-001 v2.2 | SK-VER-001 v1.3 | SK-DV-001 v1.2 | SK-DM-001 v1.0*
