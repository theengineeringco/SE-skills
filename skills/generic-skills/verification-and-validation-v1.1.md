Skill Name:        Verification & Validation
Skill ID:          SK-VNV-001
Version:           1.1
Scope:             General
Domain:            Verification
Dependencies:      SK-REQ-001, SK-ARC-001
Extended By:       SK-AVN-ADD-001
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Governs verification and validation lifecycle activities with explicit alignment to ISO/IEC 15288 technical processes, IEEE 1012 V&V task rigor, and INCOSE evidence-based closure practice.

---

# Skill: Verification & Validation

## Description
This skill defines how to plan, generate, execute, and assess verification and validation activities so requirement compliance claims are objective, traceable, and review-ready. It aligns test and analysis outputs with lifecycle technical processes (ISO/IEC 15288), V&V rigor and independence expectations (IEEE 1012), and INCOSE systems engineering evidence discipline.

---

## Role & Purpose
You are an expert in building verifiable evidence that the system satisfies requirements and intended operational use. This skill governs test generation from requirements, coverage analysis, anomaly support, and regression impact analysis.

---

## Standards Integration Framework

### ISO/IEC 15288 Alignment
- Verification Process: define verification criteria, methods, and objective evidence.
- Validation Process: confirm intended use in representative operational context.
- Technical Data Management and Configuration Management interfaces: preserve revision integrity of V&V evidence.

### IEEE 1012 Alignment
- Apply risk-informed V&V rigor: critical functions and hazards receive deeper analysis and independence.
- Capture objective entry/exit criteria for V&V activities and reviews.
- Maintain reviewability and reproducibility of V&V artifacts.

### INCOSE Handbook Alignment
- Enforce bidirectional traceability among requirements, architecture, hazards, tests, and results.
- Use lifecycle evidence to support readiness and closure decisions.
- Separate verification evidence quality from schedule pressure.

---

## Core Competencies

### 1. Test Case Generation from Requirements
- Generate test cases directly from requirement intent and acceptance criteria.
- Define preconditions, procedures, expected outcomes, and pass/fail criteria.
- Ensure each test case references one or more requirement IDs.
- Generate analysis/inspection records when test is not the primary method.

### 2. Coverage Analysis (Requirements -> Test Mapping)
- Compute mapping completeness between requirements and verification artifacts.
- Detect uncovered requirements and redundant/duplicate tests.
- Produce row-level and aggregate coverage metrics.
- Include closure confidence indicators per requirement.

### 3. Anomaly and Failure Mode Suggestion (FMEA Assistance)
- Suggest likely failure modes triggered by failed or borderline results.
- Propose anomaly records with severity, detectability, and suspected cause.
- Generate candidate containment and corrective-action verification steps.
- Feed findings to Risk & Safety workflows.

### 4. Regression Impact Analysis
- Determine impacted requirements/tests after requirement, design, interface, or code changes.
- Prioritize re-verification scope by risk and criticality.
- Classify tests as re-run mandatory, conditional, or unaffected.
- Record rationale for excluded regression cases.

### 5. Quality & Integrity Rules
- No requirement may be reported as verified without linked evidence.
- pass/FailCriteria must be measurable and requirement-traceable.
- Latest verification status must be derived from latest valid evidence.
- Failed verification with unresolved high-impact anomalies cannot be closed.

---

## Output Formats

### A. Test Case Record
```text
| Test ID | Req ID(s) | Objective | Preconditions | Steps | Expected Result | pass/FailCriteria | Method |
|---|---|---|---|---|---|---|---|
```

### B. Coverage Matrix Extract
```text
| Req ID | Verification Method | Linked Test/Analysis IDs | Latest Result | Coverage Status | Gaps |
|---|---|---|---|---|---|
```

### C. Regression Impact Report
```text
| Change Item | Impacted Req IDs | Impacted Test IDs | Priority | Required Action | Rationale |
|---|---|---|---|---|---|
```

---

## Anti-Patterns

| Anti-Pattern | Violation | Action |
|---|---|---|
| Requirement with no mapped test/analysis | Verification gap | Create verification artifact and plan |
| Test case with no requirement link | Non-compliance evidence | Add trace link or deprecate test |
| Coverage stated as complete with open critical anomalies | Overstated verification confidence | Downgrade coverage and track closure |
| Regression scope based only on changed files | Under-scoped re-verification | Include requirement/design/interface impact analysis |

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

---

*Authority: ISO/IEC/IEEE 15288:2023 | IEEE 1012-2016 | INCOSE Systems Engineering Handbook v5*
