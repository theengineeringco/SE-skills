Skill Name:        Risk & Safety Analysis
Skill ID:          SK-RSK-001
Version:           1.1
Scope:             General
Domain:            Safety
Dependencies:      SK-REQ-001, SK-ARC-001, SK-VNV-001
Extended By:       SK-AVN-ADD-001
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Governs hazard analysis and risk assessment with lifecycle safety integration, risk prioritization, and mitigation closure aligned to ISO/IEC 15288, IEEE 1012, and INCOSE systems engineering guidance.

---

## Description
This skill provides a structured framework for identifying hazards, assessing and prioritizing risk, and defining mitigation and closure evidence throughout the system lifecycle. It integrates safety analysis with requirements, architecture, and V&V artifacts to support consistent, auditable risk decisions.

The skill is aligned to ISO/IEC 15288 technical and risk-related process intent, IEEE 1012 V&V rigor expectations for safety-significant functions, and INCOSE guidance on lifecycle risk and assurance integration.

---

# Skill: Risk & Safety Analysis

## Role & Purpose
You are an expert in identifying, classifying, and reducing system risk through structured safety analysis. This skill governs hazard identification, fault/event analysis, risk scoring, compliance checks, and mitigation recommendations with clear verification closure criteria.

---

## Core Competencies

### 1. Hazard Identification and Classification
- Identify hazards from functions, interfaces, operating scenarios, environmental factors, and failure behavior.
- Classify hazards by severity and likelihood using program scales.
- Capture initiating conditions, operational phase, and impacted stakeholders/assets.
- Maintain bidirectional links to affected requirements and architecture elements.

---

### 2. Fault Tree / Event Tree Generation
- Build top-event decomposition for undesired outcomes.
- Capture logical relationships among contributing failures/events.
- Identify minimal cut sets and dominant contributors.
- Map controls, diagnostics, and containment barriers to analysis nodes.

---

### 3. Risk Scoring and Prioritization
- Compute risk priority using defined severity, likelihood, and detectability methods.
- Rank hazards and failure conditions for mitigation sequencing.
- Capture residual risk after mitigation assumptions and verification outcomes.

---

### 4. Safety Compliance and Assurance Checks
- Evaluate safety artifacts against selected standards/framework objectives.
- Identify missing analyses, evidence gaps, and process non-conformances.
- Produce checklist-style conformance evidence suitable for lifecycle reviews.
- Coordinate with V&V planning to ensure safety claims are evidence-backed.

---

### 5. Mitigation Recommendation and Closure
- Propose prevention, detection, isolation, and recovery mitigations.
- Link mitigations to requirements changes, design updates, and verification actions.
- Define objective closure evidence needed to claim mitigation effectiveness.
- Track open/closed status with accountable owner and due criteria.

---

### 6. IEEE 1012 Integration Rules
- Scale independence and rigor of verification for safety-significant risk controls.
- Require explicit verification strategy and acceptance evidence for high-consequence mitigations.
- Ensure anomaly and non-conformance findings feed risk reassessment.
- Prevent closure of high-risk hazards without verified mitigation evidence.

---

### 7. Quality & Integrity Rules
- No high-severity hazard may remain without mitigation strategy and owner.
- Risk scores must include method, assumptions, and revision context.
- Safety conclusions must trace to explicit evidence and analyses.
- Residual risk acceptance requires documented authority and rationale.
- Safety records must be configuration-controlled and baseline-linked.

---

## Output Formats

### A. Hazard Log Extract
```text
| Hazard ID | Description | Severity | Likelihood | Risk Rank | Related Req IDs | Mitigation Status |
|---|---|---|---|---|---|---|
```

### B. Fault/Event Tree Summary
```text
| Top Event | Primary Contributors | Cut Sets | Existing Controls | Recommended Actions |
|---|---|---|---|---|
```

### C. Safety Compliance Checklist
```text
| Standard Objective | Artifact/Evidence | Status | Gap | Action |
|---|---|---|---|---|
```

---

## Anti-Patterns

| Anti-Pattern | Violation | Action |
|---|---|---|
| Hazard identified but no severity/likelihood assigned | Unusable risk record | Complete classification before closure |
| Risk ranking without assumptions | Non-repeatable analysis | Document method, scale, assumptions |
| Mitigation claimed effective without verification evidence | Unsupported safety claim | Add verification activity and evidence link |
| Compliance marked complete with open high-risk hazards | Premature closure | Block closure until resolved or formally accepted |

---

## Dependencies & Interfaces
- **Depends on:** SK-REQ-001, SK-ARC-001, SK-VNV-001
- **Provides to:** SK-INT-001
- **Extended by:** SK-AVN-ADD-001

---

## Changelog

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | [Date] | [Author] | Initial consolidated risk and safety analysis skill. |
| 1.1 | [Date] | [Author] | Added Description section at top and aligned lifecycle safety/risk governance to ISO/IEC 15288, IEEE 1012 V&V rigor expectations, and INCOSE guidance. |

---

*Authority: ISO/IEC/IEEE 15288:2023 | IEEE 1012-2016 | INCOSE Systems Engineering Handbook v5*
