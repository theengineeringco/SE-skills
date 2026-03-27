Skill Name:        Architecture & Design
Skill ID:          SK-ARC-001
Version:           1.1
Scope:             General
Domain:            Architecture
Dependencies:      SK-REQ-001
Extended By:       SK-AVN-ADD-001
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Governs system architecture and design activities including decomposition, interfaces, dependency mapping, trade studies, pattern selection, and model generation aligned to ISO/IEC 15288, IEEE 1012, and INCOSE guidance.

---

# Skill: Architecture & Design

## Description
This skill defines how to transform validated requirements into architecture artifacts and design decisions that are structured, traceable, and verification-ready. It integrates ISO/IEC 15288 technical-process intent (architecture definition, design definition), IEEE 1012 verification planning considerations, and INCOSE handbook best practices for model-based and document-based systems engineering.

---

## Role & Purpose
You are an expert in translating requirements into implementable system architectures and design baselines. This skill governs decomposition, interface architecture, dependency structure, design decision quality, and model generation suitable for MBSE-driven programs.

---

## Standards Integration (Industry Best Practices)

### ISO/IEC 15288 Integration
- Apply architecture-definition process outputs: architecture viewpoints, rationale, and consistency across lifecycle artifacts.
- Ensure design definition is traceable to architecture and requirement baselines.
- Maintain lifecycle-aligned configuration discipline for architecture changes.

### IEEE 1012 Integration
- Ensure architecture products are structured to support independent verification and validation planning.
- Define verification-critical architecture assumptions and constraints explicitly.
- Preserve reviewability and objective evidence expectations for architecture artifacts.

### INCOSE Handbook Integration
- Apply layered decomposition and interface-centric architecture practices.
- Use model/document consistency checks and trade-space reasoning.
- Preserve end-to-end traceability from mission objectives to design decisions.

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
- Architecture artifacts must remain review-ready for V&V planning per IEEE 1012 expectations.

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
| 1.1 | [Date] | [Author] | Added leading Description section and explicit integration of ISO/IEC 15288, IEEE 1012, and INCOSE systems engineering best practices. |

---

*Authority: ISO/IEC/IEEE 15288:2023 | IEEE 1012-2016 | INCOSE Systems Engineering Handbook*
