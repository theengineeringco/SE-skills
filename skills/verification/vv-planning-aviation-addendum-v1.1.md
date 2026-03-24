```
Skill Name:        Verification & Validation Planning — Aviation Addendum
Skill ID:          SK-VV-001-AVN
Version:           1.1
Scope:             Aviation
Domain:            Verification
Dependencies:      SK-REQ-003, SK-REQ-003-AVN, SK-VV-001, SK-CERT-001
Extended By:       SK-VER-001-AVN
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Extends the base V&V Planning skill for FAA aviation certification programs by adding DO-178C Software Verification Plan obligations, DO-254 Hardware Verification Plan obligations, DO-160G environmental qualification integration, DAL-specific independence rules, and FAA compliance documentation requirements.
```

---

# Skill: Verification & Validation Planning — Aviation Certification Addendum

## Purpose & Relationship to Base Skill

This addendum extends SK-VV-001 for use in FAA aviation certification programs. All base skill rules — V&V strategy, plan hierarchy, test plan and test case generation, VCRM schema, closure requirements, and re-verification triggers — remain fully in force. This addendum replaces or supplements the following base skill elements with aviation-specific equivalents:

- Section A: DAL-Specific Verification Independence Rules (replaces generic assurance level rules in base Section 5)
- Section B: DO-178C Software Verification Plan Obligations (extends base Section 2 working-level plans)
- Section C: DO-254 Hardware Verification Plan Obligations (extends base Section 2 working-level plans)
- Section D: DO-160G Environmental Qualification Integration (extends base Section 3 test planning)
- Section E: FAA Compliance Documentation (extends base Section 9 compliance substantiation)
- Section F: DAL-Specific Verification Method Assignment Rules (extends base Section 1 method selection)

Where this addendum conflicts with the base skill, this addendum takes precedence for aviation certification work.

---

## Section A: DAL-Specific Verification Independence Rules

Replace the generic assurance level independence rules in SK-VV-001 Section 5 with the following DAL-specific rules for aviation programs. DAL is defined in SK-CERT-001.

**DAL A:**
Verification activities (reviews, analyses, and testing) must be performed with full independence — a person or organization separate from the developer, with no shared management chain below the program level, must independently verify all outputs. For software, DO-178C requires independent review of all software verification outputs. For hardware, DO-254 requires independent review of all verification results.

**DAL B:**
Independence is required for verification of requirements, design, and test cases. Test execution independence is required for software per DO-178C. Hardware verification per DO-254 requires independent review of verification results.

**DAL C:**
Independence is required for review of software verification output per DO-178C. Hardware verification per DO-254 requires independence for hardware design review but not necessarily for all test execution.

**DAL D:**
No formal independence requirement per DO-178C or DO-254, but internal peer review is expected practice and must be documented.

**Independence Capture — Aviation Extension:**
- Flag each requirement and associated test case with its DAL and independence requirement in the VCRM.
- Where the FAA or a DER provides independent oversight, document the oversight scope and reference the associated Issue Paper or DER authorization in the MVVP.
- Where independence is satisfied by an internal organization, document the organizational independence argument in the MVVP including the management separation evidence.

---

## Section B: DO-178C Software Verification Plan Obligations

Extend the base skill Software Verification Plan entry in Section 2 with the following DO-178C-mandated content for aviation programs.

**Software Verification Plan (SVP) — Required Content per DO-178C:**
- Software Level (DAL A–E) for each software item and the basis for the level assignment per ARP4754A.
- Complete set of DO-178C verification objectives applicable to the assigned software level, with a compliance matrix showing how each objective will be satisfied.
- Reviews planned: software requirements review, software design review, source code review, test coverage review — with independence requirements per DAL.
- Analyses planned: control flow analysis, data flow analysis, stack analysis, worst-case execution time analysis — with independence requirements per DAL.
- Structural coverage analysis requirements: statement coverage (DAL C), decision coverage (DAL B), MC/DC coverage (DAL A) — with the coverage analysis tool identified and its qualification status per DO-330.
- Test environment description: target processor, compiler, operating system, board support package — and any limitations on test environment fidelity relative to the target hardware.
- Tool qualification requirements per DO-330: identify all development and verification tools that require qualification, their Tool Qualification Level (TQL), and the qualification approach.
- Regression strategy: the criteria for re-running tests following a software change, including the structural coverage re-analysis requirements.

**DO-178C Supplement Applicability — Flag when relevant:**
- **DO-331 (Model-Based Development):** Required when a model is used to develop or verify software. The SVP must describe which DO-178C objectives are satisfied by the model-based activities and which by traditional means.
- **DO-332 (Object-Oriented Technology):** Required when OOT features (inheritance, polymorphism, dynamic memory) are used. The SVP must address additional verification objectives for OOT-specific failure modes.
- **DO-333 (Formal Methods):** Required when formal methods are used to satisfy DO-178C objectives. The SVP must describe the formal method, its tool, and how it satisfies the applicable objectives.
- **AI/ML Functions:** DO-178C does not directly address AI/ML. Where AI/ML is used in airborne software, reference FAA AC 20-115D and the current EASA AI guidance. Flag as requiring special coordination with the FAA ACO.

---

## Section C: DO-254 Hardware Verification Plan Obligations

Extend the base skill Hardware Verification Plan entry in Section 2 with the following DO-254-mandated content for aviation programs.

**Hardware Verification Plan (HVP) — Required Content per DO-254:**
- Hardware Design Assurance Level (DAL A–E) for each Complex Electronic Hardware (CEH) item and the basis for the level assignment.
- Identification of all items in scope as CEH vs. simple hardware — simple hardware does not require DO-254 but must still be shown acceptable.
- Complete set of DO-254 verification objectives applicable to the assigned DAL, with a compliance matrix.
- Hardware reviews planned: hardware requirements review, hardware design review, HDL code review — with independence requirements per DAL per FAA Order 8110.105A.
- Hardware analyses planned: worst-case analysis, failure modes and effects analysis, timing analysis — with independence requirements per DAL.
- Acceptance test requirements: the criteria and procedures for production acceptance testing of each CEH item.
- COTS component usage: identification of any COTS processors, FPGAs, or other complex components and the approach to establishing their acceptable use in the design.
- Hardware/software integration verification approach: how the interaction between hardware and software will be verified at the integrated level.

---

## Section D: DO-160G Environmental Qualification Integration

Extend the base skill test planning content (Section 3) with the following DO-160G-specific requirements for aviation programs.

**Environmental Qualification Planning:**
- For each LRU or equipment item, determine the applicable DO-160G environmental categories based on: installation location, operational environment, and aircraft certification basis. Common applicable sections include: Temperature & Altitude (Section 4), Humidity (Section 6), Vibration (Section 8), Explosion Proofness (Section 9), Waterproofness (Section 10), EMI/EMC (Sections 15, 16, 17, 18, 21), Lightning (Sections 22, 23), and Icing (Section 24).
- Document the selected DO-160G category for each applicable section in the Equipment Qualification Test Plan and trace each selection to the installation requirements and operational envelope requirements in the VCRM.
- Where environmental qualification is established by similarity, apply the similarity conditions from SK-VV-001 Section 7 and document the environmental delta analysis in the SAR.

**DO-160G Integration with System Safety:**
- EMI/EMC and lightning test categories must be selected in coordination with the system safety assessment — the selected category must protect safety-critical functions from the electromagnetic environment in the aircraft-level requirements.
- Vibration qualification categories must be validated against the aircraft structural loads analysis for the installation location.

**DO-160G VCRM Tagging:**
Add the following fields to VCRM records for DO-160G qualification requirements:

| Field | Description |
|---|---|
| DO-160G Section | Applicable DO-160G section number(s) |
| DO-160G Category | Selected qualification category for each applicable section |
| Installation Zone | Aircraft zone in which the equipment is installed |
| Environmental Qualification Report | Document ID of the approved DO-160G qualification test report |

---

## Section E: FAA Compliance Documentation

Extend the base skill compliance substantiation content (Section 9) with the following FAA-specific documentation requirements for aviation programs.

**Plan for Software / Hardware Aspects of Certification:**
- The PSAC (Plan for Software Aspects of Certification) and PHAC (Plan for Hardware Aspects of Certification) are the contracts between the developer and the FAA for DO-178C and DO-254 compliance respectively.
- The PSAC must be submitted to and agreed with the FAA ACO before software development begins. The SVP governed by Section B of this addendum is a primary input to the PSAC.
- The PHAC must be submitted to and agreed with the FAA ACO (or reviewed by the authorized DER) before hardware development begins. The HVP governed by Section C is a primary input to the PHAC.
- Changes to the PSAC or PHAC after FAA agreement require FAA notification and, for significant changes, re-agreement before implementation.

**Verification Compliance Reports (VCRs) for Aviation:**
- For each element of the agreed certification basis (per the PSCP), generate a VCR that: identifies the certification basis element, describes the verification activities conducted, references the evidence, and states the compliance finding.
- VCRs for DAL A and B items must be reviewed and found acceptable by the FAA or an authorized DER before the compliance finding may be closed.
- VCRs must be cross-referenced to the VCRM — every compliance finding in a VCR must have a corresponding Closed record in the VCRM.

**Stage of Involvement (SOI) Audit Preparation:**
- The FAA conducts SOI audits at defined program stages to verify that the development and verification processes comply with the agreed plans.
- Prepare for SOI audits by ensuring: all planning documents are approved and consistent with actual practice, the VCRM reflects current verification status, all independence records are documented, and any open findings from previous SOI audits are resolved or tracked.
- SOI audit findings must be entered as open actions in the program risk register and resolved before the subsequent program milestone.

**DER Compliance Findings:**
- Where a DER is authorized to make compliance findings on behalf of the FAA, the DER's findings and supporting review records are certification records equivalent in status to direct FAA findings.
- DER findings must be referenced in the VCR for the applicable certification basis element and retained as permanent certification records.

---

## Section F: DAL-Specific Verification Method Assignment Rules

Extend the base skill method assignment rules (Section 1) with the following DAL-specific assignment rules for aviation programs, consistent with ARP4754A Table 7 and SK-REQ-002 Section D.

| Requirement Type | DAL | Preferred Method | Acceptable Alternatives | Not Acceptable |
|---|---|---|---|---|
| FUNC | A or B | Test | Analysis (validated model) | Inspection alone, Similarity alone |
| FUNC | C or D | Test or Analysis | Inspection, Similarity | — |
| PERF | A or B | Test | Analysis (with model validation evidence) | Inspection, Demonstration |
| PERF | C or D | Test or Analysis | Demonstration | — |
| SAFE (probability target) | Any | Analysis | — | Test alone, Inspection, Similarity alone |
| SAFE (independence obligation) | Any | Analysis + Inspection | Test | — |
| INTF | A or B | Test | Analysis | Inspection alone |
| INTF | C or D | Test or Inspection | Analysis, Similarity | — |
| DERV | Any | Per functional type above | — | — |
| CONF | Any | Inspection or Analysis | — | — |

**Similarity — Aviation-Specific Restrictions:**
- Similarity shall never be assigned as the sole verification method for a DAL A safety requirement without prior FAA ACO concurrence documented in the certification plan.
- Every requirement verified by Similarity must reference the SAR ID in the VCRM.
- Where differences between the similar item and the current design affect the requirement being closed, supplemental verification activities must be added and the VCRM updated to Similarity + [supplemental method].

---

## Anti-Patterns — Aviation Additions

Add the following to the base skill anti-pattern table:

| Anti-Pattern | Violation | Action |
|---|---|---|
| PSAC or PHAC not agreed with FAA before development begins | Development proceeding without approved compliance plan | Submit PSAC/PHAC to FAA ACO for agreement before development start |
| DO-178C structural coverage not planned for DAL A/B software | MC/DC coverage requirement unaddressed | Add structural coverage analysis to SVP with tool qualification plan |
| DO-160G categories not traced to VCRM | Environmental qualification not part of compliance record | Add DO-160G records to VCRM per Section D |
| VCR compliance finding not cross-referenced to VCRM | Compliance claim without supporting traceability record | Ensure every VCR finding has a corresponding Closed VCRM entry |
| SOI audit finding not entered in risk register | Audit finding untracked — may remain open at next milestone | Enter as open risk action; resolve before subsequent milestone |
| Similarity claimed for DAL A requirement without FAA ACO concurrence | Unapproved compliance approach for safety-critical requirement | Obtain FAA ACO concurrence before closing requirement by similarity |
| AI/ML function treated as standard DO-178C software | Novel verification approach required — DO-178C insufficient | Flag for FAA ACO coordination; reference AC 20-115D |

---

## Dependencies & Interfaces

- **Extends:** SK-VV-001 — all base rules remain in force
- **Depends on:** SK-REQ-003-AVN (ARP4754A requirements traceability, safety requirement coverage), SK-CERT-001 (DAL definition, DO-178C, DO-254, DO-160G authority)
- **Coordinates with:** SK-INTF-001-AVN — DO-160G category assignments as input to environmental qualification planning
- **Coordinates with:** SK-INTF-002-AVN — conformity inspection configuration records

---

## Changelog

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | [Date] | [Author] | Initial release — content migrated from SK-VV-001 v1.0 (aviation scope) and extended with DO-178C SVP obligations, DO-254 HVP obligations, DO-160G VCRM fields, PSAC/PHAC requirements, SOI audit preparation, DER compliance finding records, and DAL-specific method assignment table. |
| 1.1 | [Date] | [Author] | Updated metadata to reflect downstream dependency: added `SK-VER-001-AVN` to `Extended By` for registry consistency. |

---

*Authority: RTCA DO-178C (2011) | RTCA DO-254 (2000) | RTCA DO-160G | FAA Order 8110.105A | SAE ARP4754A (2010) | Extends: SK-VV-001 v2.1*
