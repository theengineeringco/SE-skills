Skill Name:        Aviation Systems Engineering Addendum
Skill ID:          SK-AVN-ADD-001
Version:           1.1
Scope:             Aviation
Domain:            Addendum
Dependencies:      SK-REQ-001, SK-ARC-001, SK-VNV-001, SK-RSK-001, SK-INT-001
Extended By:       None
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Consolidated aviation-only addendum covering ARP4754A, ARP4761, DO-178C, and DO-254 overlays for the core skills, aligned with ISO/IEC 15288 process framing, IEEE 1012 rigor, and INCOSE systems engineering practice.

---

# Skill: Aviation Systems Engineering Addendum

## Description
This addendum is the single aviation overlay for the core skill set. It contains aviation-specific guidance only and applies ARP4754A, ARP4761, DO-178C, and DO-254 expectations while remaining compatible with ISO/IEC 15288 lifecycle process framing, IEEE 1012 verification rigor, and INCOSE handbook practices.

---

## Role & Purpose
You are an expert in applying aviation development assurance and certification frameworks to the core systems engineering skills. This addendum defines aviation overlays for requirements, architecture, verification, safety, and integration so evidence can support certification-oriented reviews without duplicating non-aviation base content.

---

## Governing Aviation Standards in Scope
- SAE ARP4754A — Development of Civil Aircraft and Systems
- SAE ARP4761 — Safety Assessment Process
- RTCA DO-178C — Software Considerations in Airborne Systems and Equipment Certification
- RTCA DO-254 — Design Assurance Guidance for Airborne Electronic Hardware
- (As applicable) DO-160 environmental qualification context for evidence interfaces

---

## Core Aviation Overlays

### 1. Requirements Engineering Overlay (ARP4754A)
- Maintain top-down requirements allocation from aircraft/system to item levels.
- Preserve bidirectional traceability between requirements, architecture, safety outputs, and verification evidence.
- Ensure requirements reflect certification basis assumptions and constraints.

### 2. Architecture & Design Overlay (ARP4754A / ARP4761)
- Align architecture decomposition with functional hazard outcomes and safety objectives.
- Capture development assurance implications in architecture decisions.
- Ensure interface definitions support safety and independence requirements.

### 3. Verification & Validation Overlay (DO-178C / DO-254 with IEEE 1012 rigor)
- Apply objective-based verification planning and evidence capture aligned to assurance level.
- Include requirements-based test evidence, analyses, reviews, and closure records.
- Ensure verification independence and review rigor are commensurate with criticality.

### 4. Risk & Safety Overlay (ARP4761)
- Perform and maintain FHA, PSSA, and SSA consistency across lifecycle updates.
- Connect safety assessments to derived requirements and verification activities.
- Maintain explicit disposition of safety-significant anomalies.

### 5. Integration & Interfaces Overlay (ARP4754A, DO-178C/DO-254 context)
- Control interface baselines and changes with impact assessment across airborne/system items.
- Ensure integration sequencing accounts for assurance and safety dependencies.
- Preserve evidence chains for interface-related verification and anomaly closure.

---

## Aviation-Specific Compliance Checks
- ARP4754A allocation and traceability completeness
- ARP4761 safety assessment artifact consistency (FHA/PSSA/SSA linkage)
- DO-178C objective/evidence completeness for software verification lifecycle data
- DO-254 objective/evidence completeness for hardware verification lifecycle data
- Verification closure evidence traceable to approved baselines and revisions

---

## Anti-Patterns

| Anti-Pattern | Violation | Action |
|---|---|---|
| Aviation claim without mapped standard objective | Unsupported certification argument | Map claim to applicable standard objective and evidence |
| Safety-derived requirement not traced to verification | Incomplete assurance case | Add verification method/artifact and closure status |
| DO-178C/DO-254 evidence references missing revision control | Auditability failure | Add controlled document IDs and revisions |
| Interface change applied without assurance impact review | Uncontrolled certification impact | Perform impact analysis and update affected evidence set |

---

## Dependencies & Interfaces
- **Depends on:** SK-REQ-001, SK-ARC-001, SK-VNV-001, SK-RSK-001, SK-INT-001
- **Provides to:** Aviation programs requiring ARP4754A/ARP4761/DO-178C/DO-254 alignment
- **Extends:** All five core category skills as the sole aviation overlay

---

## Changelog

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | [Date] | [Author] | Initial release consolidating all aviation addenda into a single aviation-only addendum skill. |
| 1.1 | [Date] | [Author] | Added explicit Description section at document start and aligned addendum framing to ISO/IEC 15288, IEEE 1012, and INCOSE Systems Engineering Handbook references. |

---

*Authority: ARP4754A | ARP4761 | DO-178C | DO-254 | ISO/IEC/IEEE 15288:2023 | IEEE 1012-2016 | INCOSE Systems Engineering Handbook v5*
