Skill Name:        Verification & Validation
Skill ID:          SK-VNV-001
Version:           1.3
Scope:             General
Domain:            Verification
Dependencies:      SK-REQ-001, SK-ARC-001
Extended By:       SK-AVN-ADD-001
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Governs verification and validation lifecycle activities and explicit generation of Verification Cross Reference Matrices (VCRMs) including scoped requirements, pass/fail criteria, methods, linked tests, status/results, coverage analysis, and priority-aware execution under constrained resources.

---

# Skill: Verification & Validation

## Description
This skill defines how to plan, generate, execute, and assess verification and validation activities so requirement compliance claims are objective, traceable, and review-ready. It includes explicit instructions to build a Verification Cross Reference Matrix (VCRM) for a specified scope with requirement-by-requirement status, evidence, and coverage assessment. The skill aligns with ISO/IEC 15288 lifecycle technical processes, IEEE 1012 V&V rigor, and INCOSE evidence-based closure practice.

---

## Role & Purpose
You are an expert in building verifiable evidence that the system satisfies requirements and intended operational use. This skill governs test generation from requirements, VCRM construction, coverage analysis, anomaly support, and regression impact analysis.

---

## Standards Integration Framework

### ISO/IEC 15288 Alignment
- Verification Process: define verification criteria, methods, and objective evidence.
- Validation Process: confirm intended use in representative operational context.
- Technical Data Management and Configuration Management interfaces: preserve revision integrity of V&V evidence and VCRM baselines.

### IEEE 1012 Alignment
- Apply risk-informed V&V rigor: critical functions and hazards receive deeper analysis and independence.
- Capture objective entry/exit criteria for V&V activities and reviews.
- Maintain reviewability and reproducibility of V&V artifacts and matrix evidence links.

### INCOSE Handbook Alignment
- Enforce bidirectional traceability among requirements, architecture, hazards, tests, and results.
- Use lifecycle evidence to support readiness and closure decisions.
- Separate verification evidence quality from schedule pressure.

---

## Core Competencies

### 1. VCRM Construction for a Specified Scope
Generate a Verification Cross Reference Matrix for the user-specified scope (system, subsystem, feature set, or baseline subset).

#### 1.1 Scope Rules
- Include each requirement in the specified scope exactly once in the matrix.
- Capture the requirement baseline/revision that governs the row.
- If a requirement is out-of-scope, do not include it in the VCRM body; list it in an exclusions note with rationale.

#### 1.2 Required VCRM Row Content
Every VCRM row shall include:
- Requirement ID and statement (for the specified scope)
- Requirement priority tier and disposition state (if additional candidate)
- pass/FailCriteria (measurable)
- Verification method (Test / Analysis / Inspection / Demonstration / Similarity)
- Linked test/analysis artifact IDs
- Verification status and latest result
- Coverage assessment and rationale

### 2. Priority-Aware Verification Planning
- Plan verification sequence from requirement priority tiers (P0 to P3) and accepted dispositions.
- Ensure P0 requirements have first-pass verification readiness before lower-tier execution.
- Do not schedule rejected requirements for verification unless reopened by change control.
- Track deferred requirements with explicit re-entry condition into the V&V plan.

### 3. Test Case Generation from Requirements
- Generate test cases directly from requirement intent and acceptance criteria.
- Define preconditions, procedures, expected outcomes, and pass/fail criteria.
- Ensure each test case references one or more requirement IDs.
- Generate analysis/inspection records when test is not the primary method.

### 4. Coverage Analysis (Requirements -> Test Mapping)
- Compute mapping completeness between requirements and verification artifacts.
- Detect uncovered requirements and redundant/duplicate tests.
- Produce row-level and aggregate coverage metrics.
- Include closure confidence indicators per requirement.

### 5. Verification Status and Result Roll-Up
- Derive requirement-level verification status from linked latest valid result records.
- Record latest result summary and evidence reference per requirement row.
- Prevent closure if failure conditions remain unresolved or evidence is incomplete.

### 6. Anomaly and Failure Mode Suggestion (FMEA Assistance)
- Suggest likely failure modes triggered by failed or borderline results.
- Propose anomaly records with severity, detectability, and suspected cause.
- Generate candidate containment and corrective-action verification steps.
- Feed findings to Risk & Safety workflows.

### 7. Regression Impact Analysis
- Determine impacted requirements/tests after requirement, design, interface, or code changes.
- Prioritize re-verification scope by risk and criticality.
- Classify tests as re-run mandatory, conditional, or unaffected.
- Record rationale for excluded regression cases.

### 8. Quality & Integrity Rules
- No requirement may be reported as verified without linked evidence.
- pass/FailCriteria must be measurable and requirement-traceable.
- Latest verification status must be derived from latest valid evidence.
- Failed verification with unresolved high-impact anomalies cannot be closed.
- A VCRM is incomplete if any in-scope requirement is missing a row.
- For constrained programs, P0/P1 accepted requirements must be explicitly visible in coverage roll-up reports.

---

## VCRM Generation Workflow
1. Confirm the specified scope and baseline revision.
2. Enumerate all in-scope requirements.
3. For each requirement, populate pass/fail criteria, method, linked tests, status, and result.
4. Compute per-requirement coverage rating and rationale.
5. Produce summary coverage metrics and open-gap list.
6. Run row-integrity checks (no missing mandatory fields).

### Coverage Rating Guidance
- **Full**: method defined, linked verification artifact exists, measurable criteria present, latest result supports closure.
- **Partial**: some elements present but one or more closure elements missing (for example missing latest result or incomplete criteria).
- **None**: no credible verification definition/evidence linkage.

---

## Output Formats

### A. Verification Cross Reference Matrix (VCRM)
```text
| Req ID | Requirement Statement | Priority Tier | Disposition | pass/FailCriteria | Verification Method | Linked Test/Analysis IDs | Verification Status | Latest Result | Evidence Ref | Coverage Rating | Coverage Rationale |
|---|---|---|---|---|---|---|---|---|---|---|---|
```

### B. VCRM Coverage Summary
```text
| Scope | Total Reqs | Full | Partial | None | % Full | Open Verification Gaps |
|---|---|---|---|---|---|---|
```

### C. Test Case Record
```text
| Test ID | Req ID(s) | Objective | Preconditions | Steps | Expected Result | pass/FailCriteria | Method |
|---|---|---|---|---|---|---|---|
```

### D. Regression Impact Report
```text
| Change Item | Impacted Req IDs | Impacted Test IDs | Priority | Required Action | Rationale |
|---|---|---|---|---|---|
```

---

## Anti-Patterns

| Anti-Pattern | Violation | Action |
|---|---|---|
| In-scope requirement missing from VCRM | Traceability/compliance gap | Add missing requirement row before release |
| VCRM row with empty pass/FailCriteria | Non-verifiable row | Add measurable criteria |
| Verification status asserted without linked result | Unsupported compliance claim | Link latest valid result or downgrade to pending |
| Row has method but no linked test/analysis IDs | Broken verification chain | Add artifact references or mark partial coverage |
| Coverage marked Full with unresolved critical failures | Overstated confidence | Downgrade coverage and track actions |
| Regression scope based only on changed files | Under-scoped re-verification | Include requirement/design/interface impact analysis |
| Deferred or rejected requirement treated as active verification closure | Baseline/disposition mismatch | Reconcile with disposition log before reporting status |

---

## Dependencies & Interfaces
- **Depends on:** SK-REQ-001, SK-ARC-001
- **Provides to:** SK-RSK-001, SK-INT-001
- **Extended by:** SK-AVN-ADD-001

---

## Changelog

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | [Date] | [Author] | Initial consolidated verification and validation skill. |
| 1.1 | [Date] | [Author] | Added front-loaded Description section and explicit integration of ISO/IEC 15288, IEEE 1012, and INCOSE verification best practices. |
| 1.2 | [Date] | [Author] | Added explicit VCRM generation competency and workflow covering scoped requirements, pass/fail criteria, verification method and linked test cases, verification status/results, and per-requirement coverage analysis. |
| 1.3 | [Date] | [Author] | Added priority-aware verification planning and VCRM fields for priority tier/disposition to support constrained delivery and explicit accept/reject/defer governance. |

---

*Authority: ISO/IEC/IEEE 15288:2023 | IEEE 1012-2016 | INCOSE Systems Engineering Handbook v5*
