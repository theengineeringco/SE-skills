# Skill Library — Gap Analysis
**Repository:** AI-Enabled Systems Engineering Skill Library
**Based on:** SK-REQ-001 through SK-DV-001 (9 skills, current library)
**Version:** 1.0

---

## Current Library Coverage

The current library covers the following systems engineering disciplines:

| Discipline | Coverage | Skills |
|---|---|---|
| Requirements writing | ✅ Strong | SK-REQ-001, SK-REQ-002 |
| Requirements capture & traceability | ✅ Strong | SK-REQ-003, SK-REQ-004 |
| Regulatory & certification knowledge | ✅ Strong | SK-CERT-001 |
| Verification & validation planning | ✅ Strong | SK-VV-001 |
| Interface capture & specification | ✅ Strong | SK-INTF-001 |
| Interface management | ✅ Strong | SK-INTF-002 |
| Design values governance | ✅ Strong | SK-DV-001 |
| MBSE / systems modeling | ⚠️ Partial | Referenced in SK-INTF-001 but no dedicated skill |
| System safety assessment | ⚠️ Partial | Referenced in SK-CERT-001 and SK-REQ-002 but no dedicated skill |
| Software development assurance | ⚠️ Partial | Referenced in SK-CERT-001 but no dedicated skill |
| Hardware development assurance | ⚠️ Partial | Referenced in SK-CERT-001 but no dedicated skill |
| Trade study & architecture decisions | ❌ Not covered | — |
| Configuration management | ❌ Not covered | — |
| Program planning & milestone management | ❌ Not covered | — |
| Human factors & crew interface | ❌ Not covered | — |
| Means of compliance documentation | ❌ Not covered | — |

---

## Identified Gaps

### GAP-001 — MBSE / SysML Modeling Skill
**Priority:** High
**Trigger:** SK-INTF-001 contains substantial SysML content (IBDs, BDDs, flow ports, interface blocks) that is currently embedded in an interface skill rather than governed by a dedicated modeling skill. SK-REQ-003 references MBSE allocation without modeling guidance.
**Proposed Skill:** MBSE & SysML Architecture Modeling
**Suggested Content:** SysML block hierarchy, BDD and IBD conventions, requirement allocation to model elements, interface modeling patterns, activity and state machine diagrams for functional analysis, MBSE tool conventions, and relationship between MBSE model and certification artifacts.
**Dependencies if created:** SK-REQ-003, SK-INTF-001
**Scope:** General (with aviation certification notes)

---

### GAP-002 — System Safety Assessment Skill
**Priority:** High
**Trigger:** SK-CERT-001 describes safety standards (ARP4754A, ARP4761) and SK-REQ-002 defines safety requirement patterns, but no skill governs the *conduct* of safety assessments — FHA, PSSA, SSA, FTA, FMEA, CCA. This is a major certification deliverable with no dedicated skill.
**Proposed Skill:** System Safety Assessment (FHA / PSSA / SSA / FTA / FMEA)
**Suggested Content:** FHA process and output structure, PSSA development and DAL allocation, SSA closure requirements, FTA construction and evaluation, FMEA/FMECA methodology, CCA (PRA, CMA, ZSA), quantitative probability analysis, and relationship between safety assessment outputs and requirements baseline.
**Dependencies if created:** SK-CERT-001, SK-REQ-002, SK-REQ-003
**Scope:** Aviation

---

### GAP-003 — Software Development Assurance Skill (DO-178C)
**Priority:** Medium
**Trigger:** SK-CERT-001 describes DO-178C standards knowledge but does not govern the application of DO-178C in a development program — planning documents, lifecycle data, structural coverage analysis, tool qualification, and software verification objectives.
**Proposed Skill:** Software Development Assurance (DO-178C)
**Suggested Content:** Software planning documents (PSAC, SDP, SVP, SCMP, SQAP), software lifecycle process, DAL-driven objective tables, structural coverage analysis (MC/DC), DO-330 tool qualification, DO-331/332/333 supplement applicability, and relationship between software requirements and system-level requirements.
**Dependencies if created:** SK-CERT-001, SK-REQ-003, SK-VV-001
**Scope:** Aviation

---

### GAP-004 — Hardware Development Assurance Skill (DO-254)
**Priority:** Medium
**Trigger:** SK-CERT-001 describes DO-254 standards knowledge but no skill governs the application of DO-254 in a development program — PHAC content, hardware lifecycle, CEH identification, DAL-driven objectives, and FAA Order 8110.105A compliance.
**Proposed Skill:** Hardware Development Assurance (DO-254)
**Suggested Content:** CEH identification and DAL assignment, PHAC content and structure, hardware design lifecycle (requirements, conceptual design, detailed design, implementation), hardware verification objectives by DAL, acceptance test requirements, tool qualification under DO-254, and relationship to DO-178C at hardware/software integration.
**Dependencies if created:** SK-CERT-001, SK-REQ-003, SK-VV-001
**Scope:** Aviation

---

### GAP-005 — Trade Study & Architecture Decision Skill
**Priority:** Medium
**Trigger:** No skill currently supports the structured capture and documentation of architectural trade studies and design decisions. Trade studies are the primary mechanism by which top-level requirements are translated into architecture choices, and their documentation is a certification artifact.
**Proposed Skill:** Trade Study & Architecture Decision Records
**Suggested Content:** Trade study structure (criteria definition, weighting, alternatives, scoring), Architecture Decision Record (ADR) format, traceability from trade study to requirements and design values, DAL implications of architecture decisions, and certification-relevance of trade study documentation.
**Dependencies if created:** SK-REQ-003, SK-DV-001
**Scope:** General

---

### GAP-006 — Configuration Management Skill
**Priority:** Medium
**Trigger:** Multiple skills (SK-REQ-003, SK-INTF-002, SK-DV-001, SK-VV-001) reference configuration control, baseline management, and change control processes but no skill governs the configuration management discipline itself. CM is a required element of ARP4754A and DO-178C programs.
**Proposed Skill:** Configuration Management for Certification Programs
**Suggested Content:** Configuration identification (CI selection, naming, baseline levels), configuration control (change request process, CCB), configuration status accounting, configuration audits (FCA, PCA), relationship between CM and the requirements/V&V baselines, and CM plan content.
**Dependencies if created:** SK-CERT-001, SK-REQ-003
**Scope:** Aviation (with general variant possible)

---

### GAP-007 — Means of Compliance Documentation Skill
**Priority:** Medium
**Trigger:** SK-CERT-001 describes the certification basis and MoC selection, and SK-VV-001 covers verification closure, but no skill governs the generation of the certification documentation package — Certification Plan, PSCP, compliance checklists, Issue Papers, and Verification Compliance Reports submitted to the FAA.
**Proposed Skill:** Means of Compliance & Certification Documentation
**Suggested Content:** Certification Plan and PSCP structure, Issue Paper process and content, compliance checklist generation from certification basis, Verification Compliance Report (VCR) structure, Stage of Involvement (SOI) audit preparation, and DER coordination documentation.
**Dependencies if created:** SK-CERT-001, SK-VV-001, SK-REQ-003
**Scope:** Aviation

---

### GAP-008 — Human Factors & Crew Interface Skill
**Priority:** Low–Medium
**Trigger:** No skill addresses the human factors engineering discipline — crew alerting system design, flight deck interface requirements, workload analysis, and FAA human factors certification guidance (AC 25.1302, AC 25.11). This is increasingly important for eVTOL given novel flight modes and automation levels.
**Proposed Skill:** Human Factors & Crew Interface Engineering
**Suggested Content:** Human factors requirements derivation, crew alerting system (CAS) design principles, flight deck display requirements, workload analysis methods, human error analysis, and FAA AC 25.1302 compliance approach.
**Dependencies if created:** SK-CERT-001, SK-REQ-002
**Scope:** Aviation

---

### GAP-009 — General Requirements Field Specification
**Priority:** Low
**Trigger:** SK-REQ-004 (Requirements Field Specification) is scoped to aviation certification programs. A general-purpose version applicable to non-aviation programs would extend the utility of SK-REQ-001 and SK-DV-001 as general-purpose skills.
**Proposed Skill:** Requirements Field Specification (General)
**Suggested Content:** Core field set applicable to any engineering program, with phase-gated mandatory/optional rules expressed in terms of generic program milestones rather than PDR/CDR/TRR.
**Dependencies if created:** SK-REQ-001, SK-REQ-003
**Scope:** General

---

## Overlap Analysis

| Overlap | Skills Involved | Assessment | Recommended Action |
|---|---|---|---|
| SysML interface modeling content | SK-INTF-001 contains SysML patterns that belong in a future MBSE skill | Acceptable until GAP-001 is addressed | When MBSE skill is created, migrate SysML content from SK-INTF-001 and replace with a reference |
| Safety requirement patterns | SK-CERT-001 describes safety standards; SK-REQ-002 defines safety requirement patterns | Intentional division — SK-CERT-001 is knowledge, SK-REQ-002 is authoring | No action required; document the division in both skills |
| DAL assignment logic | Appears in SK-CERT-001, SK-REQ-002, SK-REQ-004, SK-VV-001 | Acceptable repetition — each skill applies DAL in its own context | Ensure terminology is consistent across all four skills on next review |
| Verification method definitions | Defined in SK-REQ-001 (base), SK-REQ-002 (extended), SK-VV-001 (detailed) | Intentional layering | Confirm SK-VV-001 does not contradict SK-REQ-001 definitions on next review |

---

## Gap Priority Summary

| Priority | Gap IDs | Count |
|---|---|---|
| High | GAP-001, GAP-002 | 2 |
| Medium | GAP-003, GAP-004, GAP-005, GAP-006, GAP-007 | 5 |
| Low–Medium | GAP-008 | 1 |
| Low | GAP-009 | 1 |
| **Total** | | **9** |
