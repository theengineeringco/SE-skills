Skill Name:        Requirements Capture, Traceability & Management — Aviation Addendum
Skill ID:          SK-REQ-003-AVN
Version:           1.0
Scope:             Aviation
Domain:            Requirements
Dependencies:      SK-REQ-001, SK-REQ-002, SK-REQ-003, SK-CERT-001
Extended By:       None
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Extends the base Requirements Capture, Traceability & Management skill for FAA certification programs by adding ARP4754A-aligned hierarchy naming, FHA/PSSA safety requirement traceability, DAL-aware allocation rules, and regulatory completeness checking against the agreed certification basis.


---

# Skill: Requirements Capture, Traceability & Management — Aviation Certification Addendum

## Purpose & Relationship to Base Skill

This addendum extends SK-REQ-003 for use in FAA aviation certification programs. All base skill rules — requirements hierarchy structure, traceability integrity rules, gap and conflict detection, and quality principles — remain fully in force. This addendum replaces or supplements the following base skill elements with aviation-specific equivalents:

- Section 1 hierarchy level names → replaced with ARP4754A-aligned naming (Section A)
- Section 2 requirement attributes → extended with DAL, safety assessment references, and certification fields (Section B)
- Section 4 regulatory completeness → extended with PSCP/Issue Paper cross-reference (Section C)
- Adds Section D: Safety Requirements Traceability (new — not in base skill)
- Adds Section E: DAL-Aware Allocation Rules (new — not in base skill)

Where this addendum conflicts with the base skill, this addendum takes precedence for aviation certification work.

---

## Section A: ARP4754A-Aligned Requirements Hierarchy

Replace the default hierarchy level names from SK-REQ-003 Section 1 with the following aviation-standard naming. All structural rules from the base skill apply.

**Aviation Hierarchy Levels:**

- **Level 0 — Stakeholder Needs & Objectives (SNO):** As defined in SK-REQ-003 base. No aviation-specific additions at this level.

- **Level 1 — Aircraft-Level Requirements (ALR):** Top-level functional, performance, safety, and operational requirements that define what the aircraft must do and the conditions under which it must do it. These are the root of the requirements tree and the primary interface with the FAA certification basis. ALRs must collectively satisfy the agreed certification basis documented in the PSCP.

- **Level 2 — System-Level Requirements (SLR):** Requirements allocated from ALRs to specific aircraft systems (e.g., Flight Control System, Propulsion System, Energy Management System, Avionics System). Each SLR must be traceable to one or more ALRs. SLRs are the primary input to system-level FHAs and PSSAs.

- **Level 3 — Item-Level Requirements (ILR):** Requirements allocated from SLRs to subsystems, Line Replaceable Units (LRUs), or hardware/software items. ILRs feed directly into DO-178C software requirements baselines and DO-254 hardware requirements baselines.

- **Derived Requirements (any level):** As defined in SK-REQ-003 base, with the additional requirement that all derived requirements must be flagged for safety assessment review per ARP4754A, as they may introduce unanalyzed hazard contributors. The safety assessment team must be notified of all derived requirements at Level 2 and below.

**Aviation Traceability Extension:**
- Safety requirements derived from the FHA and PSSA (per ARP4754A/ARP4761) must be traceable into the requirements architecture as first-class requirements at the appropriate level. They are not managed separately from the engineering requirements baseline.
- Traceability must flow continuously: ALR → SLR → ILR → DO-178C Software Requirements or DO-254 Hardware Requirements. A break at any level is a traceability gap and a potential certification finding.

---

## Section B: Extended Requirement Attributes for Aviation Programs

Extend the base skill attribute set (SK-REQ-003 Section 2) with the following aviation-specific fields for every requirement in an aviation certification program:

| Attribute | Description | Mandatory From |
|---|---|---|
| Requirement Type | FUNC / PERF / SAFE / INTF / DERV / OPER / CONF per SK-REQ-002 Section A | SRR |
| DAL | Development Assurance Level (A–E / TBD) per ARP4754A. Definition in SK-CERT-001. | PDR (TBD permitted at SRR) |
| FHA / PSSA Reference | ID of the failure condition in the FHA or PSSA that this requirement satisfies. Mandatory for SAFE type requirements. | PDR |
| Certification Basis Reference | The specific element of the agreed certification basis (PSCP section, Issue Paper ID, Special Condition reference) that this requirement addresses. Mandatory for CONF type. | PDR |
| Failure Behavior Companion Required | Yes / No. Auto-set to Yes for all DAL A and B FUNC and INTF requirements per SK-REQ-002 Section B. | PDR |
| Failure Behavior Companion ID | ID of the companion requirement defining failure behavior. Mandatory when Failure Behavior Companion Required = Yes. | CDR |
| Safety Assessment Notified | Yes / No / N/A. Mandatory for all DERV requirements and all SAFE requirements. | PDR |

**DAL-Aware Attribute Rules:**
- DAL TBD is not permitted in Released Baseline requirements at CDR or later for SAFE, FUNC, or INTF requirement types.
- A SAFE requirement with no FHA/PSSA Reference is an orphaned safety requirement — flag as a critical traceability error.
- A CONF requirement with no Certification Basis Reference is an ungoverned compliance obligation — flag and resolve before PDR baseline.

---

## Section C: Regulatory Completeness Checking

Extend the base skill Section 4 (Regulatory / Standards Completeness) with the following aviation-specific process:

**PSCP Cross-Reference:**
- Maintain a cross-reference between every element of the agreed certification basis (as documented in the Project Specific Certification Plan) and the requirements baseline.
- Every certification basis element must have at least one corresponding requirement of type CONF or SAFE in the baseline with a Certification Basis Reference field populated.
- A certification basis element with no corresponding requirement is a regulatory coverage gap — a direct certification finding risk.

**Issue Paper Traceability:**
- Where the FAA has issued Issue Papers establishing Special Conditions or novel means of compliance, each Issue Paper commitment must be traceable to at least one requirement in the baseline.
- Issue Paper commitments not reflected in the requirements baseline represent unmanaged compliance obligations — flag and escalate to the certification lead.

**PSCP Completeness Metric:**
- At any program review milestone, report: the number of PSCP elements with at least one corresponding requirement (covered), the number with no corresponding requirement (gap), and the number with a corresponding requirement but no assigned MoC (MoC gap).

---

## Section D: Safety Requirements Traceability

This section governs the traceability of safety requirements derived from the ARP4754A/ARP4761 safety assessment process. It has no equivalent in the base skill.

**FHA Traceability:**
- Every failure condition identified in the aircraft-level FHA must have a corresponding SAFE requirement in the ALR baseline. FHA failure conditions with no corresponding ALR are safety coverage gaps.
- The FHA failure condition severity category (Catastrophic, Hazardous, Major, Minor, No Safety Effect) determines the DAL assigned to the requirement and the probability target that must be stated in the Pattern S2 requirement (per SK-REQ-002 Section C.1).

**PSSA Traceability:**
- Safety requirements derived from the PSSA (system-level safety allocation) must be traceable to their parent FHA failure condition and allocated to the correct system as SLRs.
- Independence requirements derived from the PSSA (per ARP4761 CCA) must be expressed as SAFE requirements using Pattern S3 (per SK-REQ-002 Section C.1) and entered in the SLR baseline.

**SSA Closure:**
- The System Safety Assessment (SSA) closure process requires that every SAFE requirement in the baseline has a closed verification activity in the VCRM. The requirements baseline is the input to the SSA — a SAFE requirement that is unverified at SSA closure is a program stop.

**Safety Requirement Completeness Metric:**
- Report at each milestone: total FHA failure conditions, count with corresponding SAFE requirement (covered), count without (gap), count with SAFE requirement and closed verification activity (verified).

---

## Section E: DAL-Aware Allocation Rules

This section governs how DAL assignments from the FHA/PSSA drive requirements allocation decisions. It has no equivalent in the base skill.

**DAL Allocation Integrity:**
- When a system-level requirement is allocated to a subsystem or item, the DAL of the allocated requirement must be at least as high as the DAL of the parent system-level requirement. A requirement may not be allocated to an item developed at a lower DAL than the requirement's safety objective demands.
- Where an architecture uses redundancy to achieve a safety objective, each redundant path must have its own requirement at the appropriate DAL — a single requirement covering both paths is an allocation error.

**Independence Requirements:**
- Where the PSSA requires independence between two functions, items, or development processes, the independence obligation must be expressed as an explicit SAFE requirement (Pattern S3) — not left as an architectural assumption.
- Independence requirements must trace to both the function providing independence AND the function it is independent from — single-sided independence requirements are incomplete.

**DAL Conflict Detection:**
- Flag any requirement allocated to an item at DAL B whose satisfaction depends on a software module or hardware item developed at DAL C or lower — the lower assurance level of the supporting item is insufficient to support the parent requirement's safety objective.
- Flag any architecture where a single failure in a shared resource (common power bus, common processor, common software partition) can affect two requirements that are required to be independent per the PSSA.

---

## Anti-Patterns — Aviation Additions

Add the following to the base skill anti-pattern table:

| Anti-Pattern | Violation | Action |
|---|---|---|
| SAFE requirement with no FHA/PSSA reference | Orphaned safety requirement — not traceable to safety analysis | Add FHA/PSSA reference or reclassify requirement type |
| FHA failure condition with no SAFE requirement | Safety coverage gap — direct certification risk | Generate SAFE requirement using SK-REQ-002 Pattern S1, S2, or S3 |
| DAL A/B requirement with no failure behavior companion | Incomplete safety-critical requirement set | Generate companion SAFE requirement per SK-REQ-002 Section B |
| CONF requirement with no certification basis reference | Ungoverned compliance obligation | Add PSCP section or Issue Paper ID to Certification Basis Reference field |
| PSSA independence claim with no corresponding SAFE requirement | Unmanaged independence obligation | Generate Pattern S3 requirement naming both items |
| Derived requirement at Level 2+ with safety assessment not notified | Unreviewed potential failure mode | Notify safety assessment team; update Safety Assessment Notified field |

---

## Dependencies & Interfaces

- **Extends:** SK-REQ-003 — all base rules remain in force
- **Depends on:** SK-REQ-001 (requirement writing rules), SK-REQ-002 (aviation requirement patterns), SK-CERT-001 (DAL definition, ARP4754A, ARP4761 authority)
- **Provides to:** SK-REQ-004 — aviation-specific field attributes
- **Provides to:** SK-VV-001 — safety requirement traceability as input to VCRM construction
- **Coordinates with:** SK-INTF-001 — interface requirement traceability at SLR/ILR level

---

## Changelog

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | [Date] | [Author] | Initial release — content migrated from SK-REQ-003 v1.0 (aviation scope) and extended with ARP4754A alignment, FHA/PSSA traceability, DAL allocation rules, and PSCP completeness checking. |

---

*Authority: SAE ARP4754A (2010) | SAE ARP4761 (1996) | FAA AC 25.1309-1B | FAA AC 23.1309-1E | Extends: SK-REQ-003 v2.0*
