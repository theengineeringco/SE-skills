Skill Name:        Interface Management — Aviation Addendum
Skill ID:          SK-INTF-002-AVN
Version:           1.0
Scope:             Aviation
Domain:            Interfaces
Dependencies:      SK-INTF-001, SK-INTF-001-AVN, SK-INTF-002, SK-REQ-003, SK-REQ-003-AVN, SK-CERT-001
Extended By:       None
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Extends the base Interface Management skill for FAA aviation certification programs by adding DAL-driven change control tier assignment, aviation program milestone gate criteria, FAA ACO notification requirements, and conformity inspection interface closure obligations.


---

# Skill: Interface Management — Aviation Certification Addendum

## Purpose & Relationship to Base Skill

This addendum extends SK-INTF-002 for use in FAA aviation certification programs. All base skill rules — Interface Registry, baseline control, change control tiers, supplier management, maturity metrics, and risk tracking — remain fully in force. This addendum replaces or supplements the following base skill elements with aviation-specific equivalents:

- Section A: DAL-Driven Change Control Tier Assignment (replaces generic assurance classification in base Section 3)
- Section B: Aviation Program Milestone Gate Criteria (replaces generic Review 1/2/3 in base Section 5)
- Section C: FAA ACO Notification Requirements (new — not in base skill)
- Section D: Conformity Inspection & Certification Closure (new — not in base skill)

Where this addendum conflicts with the base skill, this addendum takes precedence for aviation certification work.

---

## Section A: DAL-Driven Change Control Tier Assignment

**SE Tool Data Model Alignment:** This addendum uses the `interface` entity fields from SK-DM-001. Required fields for managed aviation interfaces include:
- `provider`, `consumer`, `interfaceType`, `direction`, `protocol/Standard`, `status`
- `ai-generated`, `aiConfidenceScore`, `humanReviewed`, `owner`
- DAL and change-control metadata captured as additional governance attributes in this skill.

Replace the generic assurance classification criterion in SK-INTF-002 Section 3 with the following DAL-specific rules for aviation programs. DAL is defined in SK-CERT-001.

**Tier 1 — Safety-Critical Interface Changes (DAL A or B interfaces, or Released Baseline ICDs):**
All Tier 1 rules from the base skill apply, plus:
- Require notification to the FAA ACO where the change affects a previously agreed Means of Compliance or a certification basis element — see Section C.
- Require the systems safety team representative on the ICB to confirm that the change impact analysis has been reviewed against the current PSSA and SSA. A change that introduces a new failure mode or alters a probability budget requires PSSA/SSA update before the ICR is approved.
- Require the certification team representative on the ICB to confirm that no Issue Paper commitment is affected. If an Issue Paper commitment is affected, FAA notification per Section C is mandatory before implementation.

**Tier 2 — Non-Safety-Critical Interface Changes (DAL C/D interfaces, Preliminary Baseline ICDs):**
All Tier 2 rules from the base skill apply. No additional aviation-specific requirements for Tier 2 changes, except that the impact assessment must confirm that the change does not affect any DAL A/B function that depends on the interface — if it does, the change is automatically reclassified as Tier 1.

**DAL Classification in the Interface Registry:**
Replace the generic "Assurance Classification" field in the base Interface Registry with:

| Field | Description |
|---|---|
| DAL Classification | The highest DAL (A–E) of any signal or function crossing this interface, per ARP4754A and SK-CERT-001 |
| Change Control Tier | Tier 1 / Tier 2 — auto-derived from DAL Classification and Baseline Status |

---

## Section B: Aviation Program Milestone Gate Criteria

Replace the generic Review 1/2/3 milestone gate criteria in SK-INTF-002 Section 5 with the following aviation-specific gate criteria tied to FAA program milestones.

**PDR (Preliminary Design Review):**
- 100% of Level 0 and Level 1 interfaces identified and entered in the Interface Registry.
- 100% of Level 0 and Level 1 ICDs at Preliminary Baseline or better.
- 80% of Level 2 interfaces identified in the Registry.
- Zero unresolved Level 0/1 interface conflicts.
- All supplier interface deliverable requirements contractually established.
- DAL classification assigned for all Level 0 and Level 1 interfaces.

**CDR (Critical Design Review):**
- 100% of interfaces at all levels identified in the Registry.
- 100% of Level 0, 1, and 2 ICDs at Released Baseline.
- 100% of Level 3 ICDs at Preliminary Baseline or better.
- Zero open TBD/TBR items on Released Baseline ICDs at Level 0–2.
- All supplier ICDs for Level 0–2 interfaces delivered and under review or approved.
- Interface verification methods assigned in the VCRM for 100% of Level 0–2 interface requirements.
- DAL classification confirmed for all interfaces at all levels.
- All Tier 1 ICR/ICN items resolved or formally tracked with disposition plan.

**TRR (Test Readiness Review):**
- 100% of all ICDs at Released Baseline.
- Zero unresolved interface conflicts at any level.
- 100% of interface requirements have assigned verification activities in the VCRM.
- Test article configuration verified to be consistent with Released Baseline ICDs — no test article may enter formal test with an unapproved interface deviation.
- All open FAA ACO interface-related actions resolved or tracked with agreed disposition.

**FAA Conformity Inspection:**
- All ICDs at Released Baseline and consistent with the conforming test article configuration.
- All interface-related Special Conditions and Issue Paper commitments have corresponding Released Baseline ICDs.
- Interface Registry reflects zero open unresolved conflicts or safety-critical open actions.
- Conformity records cross-referenced to ICD revisions for all Level 0–3 interfaces.

**Certification Closure:**
- 100% of interface requirements closed in the VCRM with verified evidence.
- All interface-related compliance findings and open items dispositioned and closed.
- Interface Registry archived as a configuration-controlled certification record per Section D.

---

## Section C: FAA ACO Notification Requirements

This section governs when and how the FAA Aircraft Certification Office (ACO) must be notified of interface changes in an aviation certification program. It has no equivalent in the base skill.

**Mandatory FAA ACO Notification Triggers:**
Notify the FAA ACO before implementing any interface change that:
- Affects a Means of Compliance (MoC) previously agreed with the FAA in the PSCP or an Issue Paper.
- Introduces a new Special Condition applicability not previously identified in the certification basis.
- Alters an interface that was specifically described in or relied upon by a previously approved compliance document (e.g., a system description in a Type Inspection Authorization or a compliance checklist).
- Changes the DAL classification of an interface from a lower to a higher DAL — this may indicate a change in the safety assessment that requires FAA review.
- Affects an interface between the aircraft and vertiport infrastructure where the interface specification has been agreed with the FAA as part of the operational approval.

**FAA Notification Process:**
- Prepare an Interface Change Summary document for the FAA ACO describing: the interface affected, the nature of the change, the impact on the certification basis, and the updated MoC.
- Submit the Interface Change Summary to the FAA ACO via the established program communication channel before implementation. Do not implement before receiving FAA acknowledgment.
- Record the FAA acknowledgment (email, meeting minutes, or formal correspondence) as a configuration-controlled program record and reference it in the ICR and the ICD change history.
- Where the change requires a formal Issue Paper revision, initiate the Issue Paper revision process in parallel with the ICR process. The ICR may not be closed until the Issue Paper revision is agreed.

**DER Coordination:**
- Where a Designated Engineering Representative (DER) has been authorized to make compliance findings on behalf of the FAA, interface changes affecting their authorization scope must be submitted to the DER for review before implementation.
- DER review records must be retained as certification records and referenced in the ICD change history.

---

## Section D: Conformity Inspection & Certification Closure

This section governs the interface management obligations specific to FAA conformity inspection and certification closure. It has no equivalent in the base skill.

**Conformity Inspection Interface Obligations:**
- Before any conformity inspection is conducted on a test article, verify that the test article's interface configuration is consistent with the Released Baseline ICDs for all interfaces on that article.
- Any deviation between the test article configuration and the Released Baseline ICD must be documented as a conformity deviation, approved by the conformity inspector, and assessed for impact on the validity of any test results obtained.
- The Interface Registry must reflect the exact ICD revision under which each conformity inspection was conducted — this is the configuration record that ties test evidence to the design definition.

**Certification Record Archiving:**
At certification closure, archive the following interface management records as permanent certification records:
- The complete Interface Registry at final revision, with all entries at status Closed or Retired.
- All Released Baseline ICDs at their final approved revision.
- All ICR/ICN records for Tier 1 changes, including FAA ACO notification records and DER review records.
- IWG minutes for all supplier interface working group meetings.
- The complete Interface Risk Register with all risks at status Closed, including closure rationale.

**Post-Certification Interface Change Obligations:**
- Any interface change after type certificate issuance constitutes a design change to the type design and must be processed as a Supplemental Type Certificate (STC) or an amendment to the existing type certificate, as appropriate.
- The Interface Management skill and associated ICR process remain applicable post-certification but operate within the STC/amendment framework rather than the initial certification program framework.

---

## Anti-Patterns — Aviation Additions

Add the following to the base skill anti-pattern table:

| Anti-Pattern | Violation | Action |
|---|---|---|
| Tier 1 ICR approved without PSSA/SSA impact confirmation | Safety assessment not updated for interface change | Require safety team sign-off on ICR before approval |
| Interface change affecting MoC implemented without FAA ACO notification | Unapproved deviation from agreed certification basis | Notify FAA ACO immediately; assess need for re-test or re-analysis |
| Test article conformity inspection conducted with unapproved interface deviation | Test evidence tied to non-conforming configuration — may be uncloseable | Document deviation, obtain conformity inspector approval, assess test validity |
| DAL classification not assigned at CDR | Unclassified interface — change control tier indeterminate | Assign DAL classification before CDR gate; flag as critical gap |
| Post-certification interface change processed as program change rather than STC | Type design changed without regulatory approval | Redirect to STC or type certificate amendment process |
| Interface Registry not archived at certification closure | Permanent certification record missing | Archive complete Registry at final revision as part of certification package |

---

## Dependencies & Interfaces

- **Extends:** SK-INTF-002 — all base rules remain in force
- **Depends on:** SK-INTF-001 (interface definitions), SK-INTF-001-AVN (DAL classification source), SK-REQ-003-AVN (PSSA/SSA traceability for change impact assessment), SK-CERT-001 (DAL definition, FAA regulatory framework)
- **Provides to:** SK-VV-001 — conformity inspection configuration records as input to test evidence validity assessment

---

## Changelog

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | [Date] | [Author] | Initial release — content migrated from SK-INTF-002 v1.0 (aviation scope) and extended with DAL-driven change control, FAA ACO notification process, conformity inspection obligations, and certification closure archiving requirements. |

---

*Authority: SAE ARP4754A (2010) | 14 CFR § 21.17(b) | FAA AC 21.17-2 | Extends: SK-INTF-002 v2.1*
