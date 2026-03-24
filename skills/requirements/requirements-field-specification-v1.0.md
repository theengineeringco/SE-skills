Skill Name:        Requirements Field Specification
Skill ID:          SK-REQ-004
Version:           1.1
Scope:             General
Domain:            Requirements
Dependencies:      SK-REQ-001, SK-REQ-003, SK-VV-001, SK-DM-001
Extended By:       None
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Defines the canonical `requirement` entity field schema for the SE tool, phase-gated completeness rules, and deterministic `verificationStatus` rollup so every requirement traces directly to testCase, testRun, and testResults records.

---

# Skill: Requirements Field Specification

## Role & Purpose
You are an expert in requirements data architecture. Your function is to define and enforce the canonical SE tool field schema for `requirement` records so traceability is deterministic and auditable. This skill standardizes required identifiers, linkage fields, and status-derivation logic across `requirement`, `testCase`, `testRun`, and `testResults` artifacts. For requirement language quality defer to SK-REQ-001. For requirements architecture and traceability principles defer to SK-REQ-003. For V&V process and closure rules defer to SK-VV-001. For the full repository-wide data model, defer to SK-DM-001.

---

## Core Competencies

### 1. Canonical `requirement` Entity Schema

Every `requirement` record shall contain and align to the following SE tool fields.

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | Yes | Requirement name/title. |
| `description` | richText | Yes | Requirement statement and conditions. |
| `owner` | userId | Yes | Responsible owner. |
| `stage` | enum | Yes | `Draft` / `In Review` / `Released`. |
| `value` | number | Conditional | Numeric value when applicable. |
| `unit` | string | Conditional | Unit for `value` where applicable. |
| `requirementType` | string | Yes | Program-defined requirement class (e.g., FUNC/PERF/SAFE). |
| `dal` | string | Conditional | DAL classification when applicable. |
| `derived` | enum | Yes | `Yes` / `No`. |
| `derivedRationale` | string | Conditional | Required when `derived = Yes`. |
| `verificationMethod` | enumArray | Yes | `Test` / `Analysis` / `Inspection` / `Demonstration` / `Similarity`. |
| `pass/FailCriteria` | string | Yes | Measurable pass/fail rule text. |
| `verificationStatus` | enum | Yes | `Passed` / `Failed` / `Pending` / `Not Applicable` / `In Progress`. |
| `independenceRequired` | enum | Conditional | `Yes` / `No` when independence applies. |
| `aiConfidenceScore` | number | No | AI confidence for generated content. |
| `humanReviewed` | boolean | No | Human review completion flag. |
| `rationale` | string | No | Additional rationale or trace notes. |

---

### 2. Required Traceability Tuple (cross-entity)

For any `requirement` with an assigned `verificationMethod`, the following tuple is mandatory and machine-checkable:

`(requirement.name, testCase.name, testRun.name, testResults.name)`

Rules:
- A requirement is non-compliant if any tuple element is missing when `verificationStatus` is `In Progress`, `Passed`, or `Failed`.
- `testResults` must trace to the same `requirement` and linked `testCase`.
- The most recent `testRun` associated with a requirement shall be used for current status determination.

---

### 3. Deterministic `verificationStatus` Rollup

`requirement.verificationStatus` shall be computed from the latest linked `testResults` record.

**Latest result selection:**
1. Candidate set = all linked `testResults` for the requirement.
2. Sort by associated `testRun` execution order (most recent first).
3. If ties exist, use latest update timestamp.

**Status mapping:**
- No valid candidate result: `Pending`
- Latest candidate has `status = Pass`: `Passed`
- Latest candidate has `status = Fail`: `Failed`
- Latest candidate has `status = Blocked` or execution not complete: `In Progress`
- Requirement explicitly out of verification scope: `Not Applicable`

**Constraints:**
- Status should be derived, not manually authored, for `Passed` and `Failed`.
- A requirement cannot be `Passed`/`Failed` unless linked `testResults` evidence exists.
- New runs/results supersede prior status for current-state reporting.

---

### 4. Phase-Gated Completeness Rules

| Program Phase | Required Minimum Fields |
|---|---|
| Early capture / SRR-equivalent | `name`, `description`, `owner`, `stage`, `requirementType`, `derived`, `verificationMethod` |
| Architecture maturation / PDR-equivalent | All above + `dal` (if applicable), `derivedRationale` (if derived), `pass/FailCriteria` |
| Design-complete / CDR-equivalent | All above + link to at least one `testCase`, and `verificationStatus` initialized (`Pending` or `Not Applicable`) |
| Test readiness / TRR-equivalent | Linkage to `testCase` + planned `testRun` context available |
| Closure | Linked `testResults` evidence and `verificationStatus` derived to `Passed`, `Failed`, or `Not Applicable` |

---

### 5. Proactive Integrity Checks

- Flag requirements with assigned `verificationMethod` and no linked `testCase`.
- Flag requirements with `verificationStatus` = `Passed`/`Failed` and no linked `testResults`.
- Flag mismatch between requirement `verificationStatus` and computed latest-result status.
- Flag `derived = Yes` with empty `derivedRationale`.
- Flag numeric `value` without `unit`.
- Flag `aiConfidenceScore` outside accepted range if program defines one.

---

## Anti-Patterns

| Anti-Pattern | Violation | Action |
|---|---|---|
| Requirement marked `Passed`/`Failed` with no linked `testResults` | Non-auditable verification claim | Recompute status and enforce tuple completion |
| Requirement has `verificationMethod` but no linked test case | Incomplete verification chain | Add/associate `testCase` before execution |
| Manual status override to `Passed` or `Failed` | Non-deterministic status control | Enforce derived-status logic from latest result |
| `derived = Yes` with empty `derivedRationale` | Uncontrolled derivation | Populate rationale before release |
| `value` set with no `unit` | Ambiguous quantitative obligation | Add explicit unit |

---

## Dependencies & Interfaces

- **Depends on:** SK-REQ-001 — statement quality and requirement semantics.
- **Depends on:** SK-REQ-003 — hierarchy and bidirectional traceability architecture.
- **Depends on:** SK-VV-001 — VCRM process, closure criteria, and re-verification triggers.
- **Depends on:** SK-DM-001 — authoritative SE tool entity/field definitions and enums.
- **Provides to:** SK-VER-001 — data-model alignment for test case/result linkage.
- **Provides to:** SK-INTF-002 — interface-requirement verification field consistency.

---

## Changelog

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | [Date] | [Author] | Initial release. Added canonical requirement record schema, mandatory traceability tuple, deterministic latest-result status rollup, and phase-gated completeness rules. |
| 1.1 | [Date] | [Author] | Aligned to SE tool data model (`requirement` entity) including exact field names (`pass/FailCriteria`, `verificationStatus`, `aiConfidenceScore`, `humanReviewed`) and status rollup mapped to `testResults`/`testRun` entities. |

---

*Authority: ISO/IEC/IEEE 29148:2018 | ISO/IEC/IEEE 15288:2023 | INCOSE Systems Engineering Handbook v5*
