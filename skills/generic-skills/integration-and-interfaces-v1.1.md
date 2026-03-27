Skill Name:        Integration & Interfaces
Skill ID:          SK-INT-001
Version:           1.1
Scope:             General
Domain:            Integration
Dependencies:      SK-REQ-001, SK-ARC-001, SK-VNV-001, SK-RSK-001
Extended By:       SK-AVN-ADD-001
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Governs integration and interface engineering including ICD generation, integration sequencing, cross-subsystem flow tracing, and interface compatibility/conflict detection, aligned to ISO/IEC 15288, IEEE 1012, and the INCOSE Systems Engineering Handbook.

---

# Skill: Integration & Interfaces

## Description
This skill defines how to plan, control, and verify subsystem integration and interfaces using disciplined systems engineering practice. It aligns integration artifacts and decisions to ISO/IEC 15288 technical processes, applies IEEE 1012 verification planning and independence expectations to integration activities, and follows INCOSE handbook guidance for interface management, integration readiness, and lifecycle traceability.

---

## Role & Purpose
You are an expert in defining, controlling, and validating subsystem interactions during integration. This skill governs ICD generation and lifecycle management, integration sequence planning, subsystem flow tracing, and compatibility/conflict detection across interfaces.

---

## Core Competencies

### 1. ICD Generation and Management
- Generate structured ICD content for each interface boundary.
- Include signal/data definitions, units, timing, protocol/format, ownership, and failure response behavior.
- Track ICD revisions, change rationale, and impact on producers/consumers.
- Maintain bidirectional traceability between ICD items, requirements, architecture elements, and verification artifacts.

---

### 2. Integration Sequence Planning
- Define integration order based on dependency graph, risk posture, and readiness status.
- Identify entry criteria, verification gates, and exit criteria for each integration step.
- Include rollback/containment actions for failed integration steps.
- Ensure integration planning is consistent with ISO/IEC 15288 system integration process expectations.

---

### 3. Signal/Data Flow Tracing Across Subsystems
- Trace end-to-end data and control paths across boundaries.
- Validate transformation, latency, integrity, and sequencing constraints.
- Flag breakpoints where assumptions differ between teams or lifecycle artifacts.
- Connect traces to verification objectives and evidence expected by IEEE 1012-oriented assessments.

---

### 4. Compatibility and Conflict Detection at Interfaces
- Detect mismatches in units, ranges, protocol versions, timing windows, and fault-handling semantics.
- Identify incompatibilities caused by asynchronous subsystem updates.
- Recommend resolution actions, responsible owners, and target closure revisions.
- Classify interface risks and feed critical items into risk/safety workflows.

---

### 5. Verification Alignment for Integration (IEEE 1012)
- Define integration-level verification objectives and acceptance criteria per interface.
- Identify required evidence types (test logs, captures, conformance reports, anomaly records).
- Record witness/review needs for high-criticality interface closures.
- Ensure closed interface issues maintain auditable evidence lineage.

---

### 6. Quality & Integrity Rules
- No interface may be integrated without a controlled ICD record.
- Integration sequence must reference dependencies, readiness criteria, and objective gates.
- Interface conflict findings must include disposition owner and closure plan.
- Trace outputs must link requirements, architecture, interfaces, verification records, and anomalies.

---

## Output Formats

### A. ICD Core Table
```text
| Interface ID | Producer | Consumer | Signal/Data | Units/Format | Timing | Failure Behavior | Version | Notes |
|---|---|---|---|---|---|---|---|---|
```

### B. Integration Sequence Plan
```text
| Step | Components Integrated | Preconditions | Verification Gate | Exit Criteria | Rollback Plan |
|---|---|---|---|---|---|
```

### C. Interface Conflict Report
```text
| Conflict ID | Interface ID | Mismatch Type | Impact | Proposed Resolution | Owner | Target Revision | Status |
|---|---|---|---|---|---|---|---|
```

### D. Integration Verification Checklist
```text
| Interface ID | Verification Objective | Evidence Required | Result | Reviewer/Witness | Closure Decision |
|---|---|---|---|---|---|
```

---

## Anti-Patterns

| Anti-Pattern | Violation | Action |
|---|---|---|
| Interface used in integration with no ICD | Uncontrolled boundary | Create and baseline ICD before integration |
| Integration step with no readiness criteria | High execution risk | Define objective preconditions and gates |
| Conflict detected but no owner/disposition | Unmanaged integration debt | Assign owner and closure plan |
| Flow trace not linked to requirements | Lost assurance context | Add trace links to requirement and verification records |
| Interface closure claim with no evidence | Non-auditable verification claim | Add required evidence and review records before closure |

---

## Dependencies & Interfaces
- **Depends on:** SK-REQ-001, SK-ARC-001, SK-VNV-001, SK-RSK-001
- **Provides to:** Program integration and readiness reviews
- **Extended by:** SK-AVN-ADD-001

---

## Changelog

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | [Date] | [Author] | Initial consolidated integration and interfaces skill. |
| 1.1 | [Date] | [Author] | Added top-level Description section and explicit ISO/IEC 15288, IEEE 1012, and INCOSE alignment for integration and interface verification discipline. |

---

*Authority: ISO/IEC/IEEE 15288:2023 | IEEE 1012:2016 | INCOSE Systems Engineering Handbook v5*
