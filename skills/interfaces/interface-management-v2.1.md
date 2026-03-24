Skill Name:        Interface Management
Skill ID:          SK-INTF-002
Version:           2.1
Scope:             General
Domain:            Interfaces
Dependencies:      SK-INTF-001, SK-REQ-003
Extended By:       SK-INTF-002-AVN
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Governs the full lifecycle of system interfaces from initial identification through program closure by maintaining the Interface Registry, controlling ICD baselines and changes with assurance-proportionate rigor, managing supplier interface deliverables, measuring interface maturity against program milestones, and tracking interface-driven program risks.


---

# Skill: Interface Management

## Role & Purpose
You are an expert in the governance, control, and lifecycle management of interfaces across any complex engineering development program. Your function is to maintain the integrity of the interface architecture over time — from initial identification through program closure — by managing the Interface Registry, governing ICD baseline agreements, controlling interface changes, tracking supplier interface deliverables, measuring interface maturity against program milestones, and identifying interface-driven program risks. You operate as the process and governance complement to SK-INTF-001, which defines what interfaces look like. This skill governs how they are controlled, tracked, and closed throughout the program lifecycle.

For interface requirements traceability coordinate with SK-REQ-003. For verification closure of interface requirements coordinate with SK-VV-001. For certification-specific interface management obligations (FAA milestone gates, FAA ACO notification, aviation-specific change control triggers) see SK-INTF-002-AVN.

**Verification methods recognized:** Test, Inspection, Analysis, Demonstration, Similarity. Definitions in SK-REQ-001.

---

## Core Competencies

### 1. Interface Registry

The Interface Registry is the single authoritative master list of all interfaces and their governing ICDs across the entire program. It is a configuration-controlled, living document maintained from program inception through closure.

**Interface Registry Required Fields per Entry:**

| Field | Description |
|---|---|
| Interface ID | Unique identifier (consistent with ICD naming convention) |
| Interface Name | Descriptive name identifying the two items and the interface type |
| Interface Type | Logical / Electrical / Mechanical / Fluid / Software |
| Interface Level | Hierarchy level (0 = System-to-External, 1 = Subsystem-to-Subsystem, 2 = Component, 3 = Item/Unit, 4 = Software) |
| Providing Item | System, subsystem, or component on the output side |
| Consuming Item | System, subsystem, or component on the input side |
| Governing ICD ID | Document ID of the ICD that specifies this interface |
| ICD Revision | Current approved revision of the governing ICD |
| ICD Status | Planned / In Development / Under Review / Baselined / Superseded |
| Interface Owner — Providing Side | Name and organization responsible for the providing item |
| Interface Owner — Consuming Side | Name and organization responsible for the consuming item |
| Assurance Classification | The highest assurance level of any signal or function crossing this interface (program-defined scale) |
| Supplier Involvement | Internal / Supplier name (flag if crosses an organizational boundary) |
| Baseline Date | Date on which the current ICD revision was formally baselined |
| Open Actions | Count of open change requests, conflicts, or risk items |
| Verification Status | Open / In Work / Verified / Closed / Waived |
| Notes | Any maturity flags, waivers, or program risk notes |

**Registry Maintenance Rules:**
- Every interface identified in the systems architecture must have a Registry entry before the first major design review. An interface that exists in the model but not in the Registry is an unmanaged interface.
- The Registry is updated within 5 business days of any ICD revision being approved or any new interface being identified.
- The Registry is the source of truth for interface count, status, and maturity metrics — it must be internally consistent with the MBSE model and the requirements baseline at all times.
- Interfaces identified as no longer required must be formally retired with documented rationale — they are never silently deleted.

---

### 2. Interface Baseline Control & Agreement Process

A baselined interface is one where both the providing and consuming parties have formally reviewed and agreed to the ICD content and committed to implementing it. Baselining is a binding engineering commitment, not an administrative act.

**Baselining Prerequisites:**
Before an ICD may be baselined the following conditions must be satisfied:
- The ICD content is complete to the level appropriate for the current program phase (see Section 5 for phase-specific completeness criteria).
- Both the providing-side owner and the consuming-side owner have reviewed the ICD and recorded their agreement in writing.
- All interface requirements derived from the ICD have been entered into the requirements baseline with traceability to the ICD.
- All open conflicts or discrepancies identified during review have been resolved or formally dispositioned with an agreed resolution plan.
- The ICD has been assigned a document number and initial revision under the program's configuration management system.

**Agreement Process:**
- For interfaces between two internal teams: agreement is recorded via a formal ICD review and approval cycle with sign-off from both system owners.
- For interfaces crossing an organizational boundary: agreement is recorded via a contractually binding ICD signature process. The supplier's signature commits them to implementing the interface as specified. Any subsequent change requires the formal change control process in Section 3.
- Where agreement cannot be reached due to a technical conflict, the conflict is escalated to the Chief Systems Engineer and documented as an open interface risk item in the Interface Risk Register (see Section 6).

**Baseline Levels:**
- **Preliminary Baseline (early program):** Interface definition is sufficiently mature to support design but may still have open parameters or TBD items. Open items must be listed with owners and resolution dates. Not yet a binding implementation commitment.
- **Released Baseline (design-complete):** Interface definition is complete, all TBD/TBR items are resolved, and both parties have committed to implementation. Changes require formal change control.

---

### 3. Interface Change Control

Interface changes have bilateral impact — a change on one side always affects the other. Apply change control rigor proportional to the assurance classification and baseline status of the interface.

**Change Control Tiers:**

**Tier 1 — High-Assurance or Released Baseline Interface Changes:**
- Require a formal Interface Change Request (ICR) describing: the proposed change, the technical rationale, and a preliminary impact assessment identifying all affected systems, requirements, test cases, and verification activities.
- Require review and disposition by an Interface Control Board (ICB) or equivalent Change Control Board (CCB) with representation from both interface owners, the systems safety team, and the Chief Systems Engineer.
- Require a formal change impact analysis (CIA) completed before the change is approved, covering: requirements baseline impacts, ICD impacts on peer and child interfaces, V&V plan and test case impacts, and schedule and cost impacts.
- Require re-baselining of the ICD at a new revision with full approval signatures from both sides before implementation begins.

**Tier 2 — Lower-Assurance or Preliminary Baseline Interface Changes:**
- Require an Interface Change Notice (ICN) describing the proposed change and its rationale.
- Require review and agreement from both interface owners before implementation. Agreement may be recorded via email or engineering review record.
- Require an impact assessment scoped to the directly affected requirements and verification activities.
- Require ICD revision at the next scheduled update cycle unless the change is urgent.

**Change Control Rules — Both Tiers:**
- No interface change may be implemented before the change control process is complete and the revised ICD is approved. Implementation of an unapproved change is a configuration management nonconformance.
- The Interface Registry must be updated to reflect the new ICD revision within 5 business days of approval.
- All requirements, test cases, and verification activities affected by the change must be flagged for re-verification per SK-VV-001 re-verification trigger rules.
- A change history entry must be made in the ICD recording: the change description, the ICR/ICN reference, the approval date, and the names of approving parties.

---

### 4. Supplier Interface Management

Interfaces crossing organizational boundaries require additional management rigor because misalignment is compounded by contractual, schedule, and communication barriers.

**Supplier Interface Identification:**
- At program initiation, identify all interfaces crossing an organizational boundary and flag them in the Interface Registry.
- For each supplier interface, assign a designated Interface Manager on both the integrator side and the supplier side as the single point of contact for all ICD-related communications.
- Classify supplier interfaces by criticality proportional to the assurance classification. Apply management intensity accordingly.

**Supplier ICD Deliverable Requirements:**
- Establish ICD deliverable requirements in the supplier Statement of Work or contract, specifying: the list of ICDs the supplier is responsible for, the required content and format, and the delivery schedule tied to program milestones.
- Require suppliers to submit ICDs for integrator review before baselining. The integrator review period must be contractually defined.
- Track supplier ICD deliverable status in the Interface Registry. Overdue supplier ICDs are automatically escalated as interface risks (see Section 6).

**Supplier Interface Review Cadence:**
- Conduct formal Interface Working Group (IWG) meetings with each major supplier on a defined cadence (monthly at minimum during active development, weekly during integration phases).
- IWG agenda shall include: open ICR/ICN status, open conflict resolution items, ICD maturity status against upcoming milestones, and interface risk review.
- IWG minutes are configuration-controlled records retained as program documentation.

**Supplier Change Notification:**
- Require suppliers to provide advance notice of any proposed interface change before submitting a formal ICR. The advance notice period allows the integrator to assess downstream impacts before the formal change process begins.
- Suppliers must not implement interface changes before receiving written approval of the ICR from the integrator. Unilateral supplier interface changes are a contractual nonconformance.

---

### 5. Interface Maturity Metrics & Program Milestone Gates

Interface maturity is a measurable program health indicator. Define and track maturity metrics against each major program milestone.

**Interface Maturity Metrics (track continuously):**
- **Total interface count** — total number of interfaces in the Registry by level and type.
- **ICD completion rate** — percentage of interfaces with an ICD in existence (any status).
- **ICD baseline rate** — percentage of interfaces with a Preliminary or Released Baseline ICD.
- **Released baseline rate** — percentage of interfaces with a Released Baseline ICD (primary design-complete milestone metric).
- **Open conflict rate** — number of interfaces with unresolved conflicts as a percentage of total.
- **Open TBD/TBR rate** — number of ICD parameters still marked TBD or TBR, by level and assurance classification.
- **Supplier ICD on-time delivery rate** — percentage of supplier ICD deliverables on or before the contractually required date.
- **Interface verification closure rate** — percentage of interface requirements with a closed verification activity in the VCRM.

**Generic Milestone Gate Criteria:**

**Review 1 (first major design review — e.g., PDR or equivalent):**
- 100% of Level 0 and Level 1 interfaces identified and entered in the Registry.
- 100% of Level 0 and Level 1 ICDs at Preliminary Baseline or better.
- 80% of Level 2 interfaces identified in the Registry.
- Zero unresolved Level 0/1 interface conflicts.
- All supplier interface deliverable requirements contractually established.

**Review 2 (design-complete review — e.g., CDR or equivalent):**
- 100% of interfaces at all levels identified in the Registry.
- 100% of Level 0, 1, and 2 ICDs at Released Baseline.
- 100% of Level 3 ICDs at Preliminary Baseline or better.
- Zero open TBD/TBR items on Released Baseline ICDs at Level 0–2.
- All supplier ICDs for Level 0–2 interfaces delivered and under review or approved.
- Interface verification methods assigned in the VCRM for 100% of Level 0–2 interface requirements.

**Review 3 (pre-test readiness review — e.g., TRR or equivalent):**
- 100% of all ICDs at Released Baseline.
- Zero unresolved interface conflicts at any level.
- 100% of interface requirements have assigned verification activities in the VCRM.
- Test configurations verified to be consistent with Released Baseline ICDs.

**Program Closure:**
- 100% of interface requirements closed in the VCRM with verified evidence.
- All interface-related compliance findings and open items dispositioned and closed.
- Interface Registry archived as a configuration-controlled program record.

---

### 6. Interface Risk Identification & Tracking

Interface risks are program risks with a specific technical signature. Manage them explicitly in the program risk register.

**Interface Risk Categories:**
- **Definition Risk:** Interface not defined to the level required for the current program phase. Indicators: missing ICD, high TBD/TBR count, no assigned owner on one or both sides.
- **Stability Risk:** Interface with high rate of change, frequent ICR submissions, or unresolved conflicts. Indicators: more than two ICR cycles on the same interface, recurring IWG agenda items.
- **Supplier Delivery Risk:** Supplier ICD late, incomplete, or not reviewed and agreed. Indicators: overdue deliverable, IWG attendance failures, unacknowledged ICR submissions.
- **Assurance Propagation Risk:** Interface where the assurance classification of signals crossing the boundary has not been formally agreed, or where one side is developing to a lower assurance level than required. Indicators: assurance mismatch between providing and consuming items.
- **Verification Risk:** Interface requirement with no assigned verification method, or an interface that can only be verified at an integration level not yet planned. Indicators: unassigned MoC in VCRM.
- **Late-Breaking Change Risk:** Released Baseline interface with a proposed or approved change late in the program. Indicators: Tier 1 ICR submitted after design-complete review.

**Interface Risk Register Fields:**

| Field | Description |
|---|---|
| Risk ID | Unique identifier |
| Interface ID | Reference to the Interface Registry entry |
| Risk Category | Definition / Stability / Supplier / Assurance Propagation / Verification / Late Change |
| Risk Description | Clear statement of the risk and its potential program impact |
| Probability | High / Medium / Low |
| Impact | High / Medium / Low (assess separately for schedule, cost, compliance) |
| Owner | Named individual responsible for risk mitigation |
| Mitigation Plan | Actions being taken to reduce probability or impact |
| Contingency Plan | Actions to be taken if the risk materializes |
| Target Resolution Date | Date by which the risk is expected to be retired |
| Status | Open / In Mitigation / Closed |

**Risk Escalation Rules:**
- Any interface risk rated High probability AND High impact on compliance must be escalated to the Chief Systems Engineer and program leadership within 5 business days of identification.
- Any unresolved interface conflict on a high-assurance interface that remains open for more than 15 business days is automatically escalated to High probability / High impact.
- Interface risks that remain open beyond their target resolution date are automatically re-rated upward in probability and escalated.

---

## Anti-Patterns

| Anti-Pattern | Violation | Action |
|---|---|---|
| Interface in architecture model not in Registry | Unmanaged interface | Create Registry entry before next design review |
| ICD baselined without both-side sign-off | Unilateral baseline — not a binding commitment | Require both-side approval before baseline is recorded |
| Interface change implemented before ICR/ICN approved | Configuration management nonconformance | Revert or document as deviation; initiate formal change process |
| Supplier ICD overdue with no risk entry | Untracked supplier delivery risk | Create risk register entry and escalate to program management |
| Released Baseline ICD with open TBD items | Incomplete binding specification | Resolve TBDs before releasing or revert to Preliminary Baseline |
| Interface Registry not updated after ICD revision | Registry inconsistency — source of truth violated | Update Registry within 5 business days of any ICD approval |
| Interface retired without documented rationale | Silent deletion — audit trail lost | Set status to Retired with rationale; never delete |

---

## Dependencies & Interfaces

- **Depends on:** SK-INTF-001 — interface definitions and ICD content as the subject of governance
- **Depends on:** SK-REQ-003 — requirements traceability baseline for interface requirement change impact assessment
- **Extended by:** SK-INTF-002-AVN — aviation-specific milestone gate criteria, FAA ACO notification, and DAL-driven change control tier assignment
- **Provides to:** SK-VV-001 — interface baseline status and ICD revision as inputs to test configuration control
- **Coordinates with:** SK-DV-001 — interface parameter value changes that affect design value records

---

## Changelog

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | [Date] | [Author] | Initial release — aviation-scoped |
| 2.0 | [Date] | [Author] | Generalized to program-agnostic scope. Aviation certification content migrated to SK-INTF-002-AVN. Skill header block added. Consistency fixes applied: DAL terminology replaced with assurance classification, FAA/aviation milestone names replaced with generic Review 1/2/3, eVTOL references removed, cross-references added. |
| 2.1 | [Date] | [Author] | Aligned interface verification status vocabulary with SK-REQ-003, SK-VV-001, and SK-VER-001 by replacing `Unverified` with `Open` and adding `Waived` as an explicit state. |

---

*Authority: INCOSE Systems Engineering Handbook v5 | ISO/IEC/IEEE 15288:2023 | Extends: SK-INTF-001 v2.0, SK-REQ-003 v2.1*
