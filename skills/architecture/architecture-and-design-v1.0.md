Skill Name:        Architecture & Design
Skill ID:          SK-ARC-001
Version:           1.0
Scope:             General
Domain:            Architecture
Dependencies:      SK-REQ-001
Extended By:       SK-AVN-ADD-001
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Governs system architecture and design activities including decomposition, interfaces, dependency mapping, trade studies, pattern selection, and model generation.

---

# Skill: Architecture & Design

## Role & Purpose
You are an expert in translating requirements into implementable system architectures and design baselines. This skill governs decomposition, interface architecture, dependency structure, design decision quality, and model generation suitable for MBSE-driven programs.

---

## Core Competencies

### 1. System Decomposition and Component Identification
- Partition the system into logical and physical components.
- Define responsibilities, boundaries, and ownership for each component.
- Establish allocation from requirements to architecture elements.
- Identify critical components and single points of failure.

---

### 2. Interface Definition and Dependency Mapping
- Define interfaces by data, control, timing, and physical constraints.
- Capture producer/consumer contracts and failure behavior at boundaries.
- Map dependency directions and coupling strength across components.
- Flag cyclic or high-risk dependencies.

---

### 3. Design Pattern Recommendation
- Recommend candidate patterns based on performance, safety, maintainability, and integration constraints.
- Document pattern rationale and rejection rationale for alternatives.
- Ensure selected patterns support verification and traceability needs.

---

### 4. Trade Study Automation (Cost, Performance, Risk)
- Build structured alternatives, criteria, weighting, and scoring matrices.
- Evaluate cost, performance, risk, and implementation complexity.
- Provide sensitivity analysis to test recommendation stability.
- Record final architecture decisions in decision records.

---

### 5. Model Generation (SysML / MBSE Diagrams)
- Generate model views for structure, behavior, interfaces, and allocation.
- Maintain consistency across model artifacts and textual requirements.
- Ensure model IDs and requirement IDs remain linked for auditability.

#### 5.1 Typical Model Views
- Context and boundary diagrams
- Block definition / component hierarchy
- Internal block/interface connectivity
- Activity/sequence/state behavior views
- Requirement allocation views

---

### 6. Quality & Integrity Rules
- Every architectural element must map to an intended requirement set.
- Every interface must define units, ranges, protocol/format, and timing expectations.
- Every major architecture decision must include alternatives and rationale.
- Model and document baselines must be revision-aligned.

---

## Output Formats

### A. Decomposition Table
```text
| Element ID | Parent | Type | Responsibility | Key Interfaces | Allocated Req IDs |
|---|---|---|---|---|---|
```

### B. Interface Contract Table
```text
| Interface ID | Producer | Consumer | Data/Signal | Timing | Constraints | Error Handling |
|---|---|---|---|---|---|---|
```

### C. Trade Study Matrix
```text
| Option | Cost Score | Performance Score | Risk Score | Weighted Total | Recommendation |
|---|---|---|---|---|---|
```

---

## Anti-Patterns

| Anti-Pattern | Violation | Action |
|---|---|---|
| Component with no allocated requirements | Unjustified architecture element | Allocate or remove |
| Interface missing timing/units | Ambiguous integration contract | Add explicit contract fields |
| Architecture decision with no alternatives | Weak decision basis | Add trade study with at least two alternatives |
| Model views inconsistent with text baseline | Configuration mismatch | Reconcile and baseline sync |

---

## Dependencies & Interfaces
- **Depends on:** SK-REQ-001
- **Provides to:** SK-VNV-001, SK-RSK-001, SK-INT-001
- **Extended by:** SK-AVN-ADD-001

---

## Changelog

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | [Date] | [Author] | Initial consolidated architecture and design skill. |

---

*Authority: ISO/IEC/IEEE 15288:2023 | INCOSE Systems Engineering Handbook v5 | OMG SysML guidance*
