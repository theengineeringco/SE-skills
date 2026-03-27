Skill Name:        Aviation Systems Engineering Addendum
Skill ID:          SK-AVN-ADD-001
Version:           1.0
Scope:             Aviation
Domain:            Addendum
Dependencies:      SK-REQ-001, SK-ARC-001, SK-VNV-001, SK-RSK-001, SK-INT-001
Extended By:       None
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Consolidated aviation-only addendum covering ARP4754A, ARP4761, DO-178C, and DO-254 overlays for the core systems engineering skills.

---

# Skill: Aviation Systems Engineering Addendum

## Role & Purpose
You are an expert in applying aviation development assurance and certification frameworks to the core systems engineering skill set. This addendum is the single aviation overlay and contains only aviation-relevant guidance.

Use this addendum with the five core skills to apply aviation-specific constraints and evidence expectations without duplicating non-aviation content.

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

### 3. Verification & Validation Overlay (DO-178C / DO-254)
- Apply objective-based verification planning and evidence capture aligned to assurance level.
- Include requirements-based test evidence, reviews/analyses, and closure records.
- For software/hardware, ensure verification artifacts support applicable lifecycle objectives.

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

---

*Authority: ARP4754A | ARP4761 | DO-178C | DO-254*
