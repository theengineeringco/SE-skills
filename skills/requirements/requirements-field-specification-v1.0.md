Skill Name:        Requirements Field Specification
Skill ID:          SK-REQ-004
Version:           1.0
Scope:             General
Domain:            Requirements
Dependencies:      SK-REQ-001, SK-REQ-003, SK-VV-001
Extended By:       None
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Defines the canonical requirements record schema, phase-gated completeness rules, and deterministic verification-status rollup logic so every requirement can be traced directly to test cases, test runs, and verification results.

---

# Skill: Requirements Field Specification

## Role & Purpose
You are an expert in requirements data architecture. Your function is to define and enforce the canonical field schema for requirement records used across the skill library so traceability is deterministic and auditable. This skill standardizes required identifiers, linkage fields, and status-derivation logic across requirements, VCRM, and verification artifacts. For requirement language quality defer to SK-REQ-001. For requirements architecture and traceability principles defer to SK-REQ-003. For V&V process and closure rules defer to SK-VV-001.

---

## Core Competencies

### 1. Canonical Requirement Record Schema

Every requirement record shall contain the following fields.

| Field | Type | Required | Description |
|---|---|---|---|
| `requirement_id` | String | Yes | Unique requirement identifier in program format (e.g., SYS-001). |
| `requirement_statement` | Text | Yes | Requirement text compliant with SK-REQ-001. |
| `source_ref` | String/List | Yes | Origin reference (stakeholder need, regulation, decision record). |
| `allocation` | String/List | Yes | Owning system/item/component responsible for satisfaction. |
| `verification_method` | Enum/List | Yes | `Test` / `Inspection` / `Analysis` / `Demonstration` / `Similarity`. |
| `verification_status` | Enum | Yes | `Open` / `In Work` / `Verified` / `Closed` / `Waived`. |
| `parent_requirement_ids` | List | Conditional | Required unless `derived_flag = true`. |
| `child_requirement_ids` | List | No | Downstream decomposition references. |
| `derived_flag` | Boolean | Yes | True if requirement is design-derived. |
| `derivation_rationale` | Text | Conditional | Required when `derived_flag = true`. |
| `vcrm_record_ids` | List | Yes | Linked VCRM rows for this requirement. Non-empty when verification method is assigned. |
| `test_case_ids` | List | Yes | Linked test case / analysis record IDs. Non-empty when verification method is assigned. |
| `latest_test_run_id` | String | Conditional | Required when status is `In Work` or beyond. |
| `latest_verification_result_id` | String | Conditional | Required when status is `In Work` or beyond. |
| `baseline_status` | Enum | Yes | `Draft` / `Preliminary Baseline` / `Released Baseline` / `Superseded`. |
| `change_history_ref` | List | No | Change record IDs that modified the requirement. |
| `design_value_ids` | List | No | Referenced design value IDs where numeric thresholds apply. |

---

### 2. Required Traceability Tuple

For any requirement with an assigned verification method, the following tuple is mandatory and machine-checkable:

`(requirement_id, vcrm_record_id, test_case_id, latest_test_run_id, latest_verification_result_id)`

Rules:
- A requirement is non-compliant if any element of the tuple is missing when status is `In Work`, `Verified`, `Closed`, or `Waived`.
- `latest_verification_result_id` must reference a result that links to the same `requirement_id`, `vcrm_record_id`, and `test_case_id`.
- `latest_test_run_id` must match the parent run of `latest_verification_result_id`.

---

### 3. Deterministic Verification Status Rollup

Requirement status shall be computed from the latest non-superseded verification result.

**Latest result selection:**
1. Candidate set = all linked results for the requirement that are not superseded.
2. Sort by `executed_at` descending.
3. If process requires independent review, break ties using `reviewed_at` descending.

**Status mapping:**
- No valid candidate result: `Open`
- Latest candidate exists but closure criteria incomplete: `In Work`
- Latest candidate passes criteria and required reviews complete: `Verified`
- VCRM closure complete with approved evidence: `Closed`
- Approved waiver/deviation recorded: `Waived`

**Constraints:**
- Status must be derived, not manually authored, for `Verified`, `Closed`, and `Waived`.
- A requirement cannot be `Closed` unless `latest_verification_result_id` and `vcrm_record_ids` are populated and consistent.
- Closed evidence is immutable; re-verification creates a new result and updates latest pointers.

---

### 4. Phase-Gated Completeness Rules

| Program Phase | Required Minimum Fields |
|---|---|
| Early capture / SRR-equivalent | `requirement_id`, `requirement_statement`, `source_ref`, `allocation`, `verification_method`, `derived_flag` |
| Architecture maturation / PDR-equivalent | All above + `parent_requirement_ids` or derivation rationale, `vcrm_record_ids`, initial `test_case_ids` |
| Design-complete / CDR-equivalent | All above + full traceability tuple except latest run/result if execution not started |
| Test readiness / TRR-equivalent | Full traceability tuple populated for in-scope executable requirements |
| Closure | Full traceability tuple + `verification_status` derived to `Closed` or `Waived` with approved evidence |

---

### 5. Proactive Integrity Checks

- Flag requirements with assigned verification method and empty `vcrm_record_ids`.
- Flag requirements with assigned verification method and empty `test_case_ids`.
- Flag status `Verified`/`Closed`/`Waived` with missing latest result pointer.
- Flag mismatch between requirement status and computed latest-result status.
- Flag broken references (IDs not found in baseline).
- Flag numeric requirement thresholds with no linked `design_value_ids`.

---

## Anti-Patterns

| Anti-Pattern | Violation | Action |
|---|---|---|
| Requirement marked `Closed` without latest verification result ID | Non-auditable closure claim | Recompute status and enforce tuple completion |
| Requirement has VCRM row but no linked test case IDs | Incomplete verification chain | Add/associate test cases before execution |
| Manual status override to `Verified` or `Closed` | Non-deterministic status control | Enforce derived-status logic from latest result |
| Broken tuple reference (run/result points to different requirement) | Traceability corruption | Quarantine record and repair links before use |
| Released baseline requirement with unresolved parent/derived basis | Uncontrolled origin | Add parent linkage or derivation rationale |

---

## Dependencies & Interfaces

- **Depends on:** SK-REQ-001 — statement quality and requirement semantics.
- **Depends on:** SK-REQ-003 — hierarchy and bidirectional traceability architecture.
- **Depends on:** SK-VV-001 — VCRM process, closure criteria, and re-verification triggers.
- **Provides to:** SK-VER-001 — data-model alignment for test case/result linkage.
- **Provides to:** SK-INTF-002 — interface-requirement verification field consistency.

---

## Changelog

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | [Date] | [Author] | Initial release. Added canonical requirement record schema, mandatory traceability tuple, deterministic latest-result status rollup, and phase-gated completeness rules. |

---

*Authority: ISO/IEC/IEEE 29148:2018 | ISO/IEC/IEEE 15288:2023 | INCOSE Systems Engineering Handbook v5*
