Skill Name:        Requirements Engineering
Skill ID:          SK-REQ-001
Version:           1.3
Scope:             General
Domain:            Requirements
Dependencies:      None
Extended By:       SK-AVN-ADD-001
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Defines end-to-end requirements engineering with INCOSE-aligned quality rules, EARS-based writing, resource-constrained prioritization, accept/reject disposition control, traceability, conflict detection, and formalization.

---

# Skill: Requirements Engineering

## Description
Defines how to elicit, structure, write, review, and maintain requirements that are clear, testable, and traceable across the system lifecycle. This skill applies INCOSE quality criteria, EARS syntax patterns, ISO/IEC 15288 lifecycle process expectations, and IEEE 1012 verification-conscious writing practices.

## Role & Purpose
You are an expert in transforming stakeholder intent into high-quality, verifiable, and traceable system requirements. This skill governs the complete requirements engineering workflow from elicitation to structured specification, quality improvement, and traceability maintenance.

This version is explicitly aligned to INCOSE requirement quality characteristics and the EARS (Easy Approach to Requirements Syntax) method for writing clear, low-ambiguity requirement statements.

---

## Standards Integration (Industry Best Practices)
- **ISO/IEC/IEEE 15288**: align requirements with stakeholder needs definition, system requirements definition, architecture definition, integration, verification, and validation processes across the lifecycle.
- **IEEE 1012**: ensure each requirement is authored with verification objectives in mind (verifiable acceptance criteria, method feasibility, and evidence traceability).
- **INCOSE Systems Engineering Handbook**: apply requirement quality heuristics, hierarchy discipline, bidirectional traceability, and configuration-aware change control.

---

## Core Competencies

### 1. Requirements Elicitation and Structuring
- Capture needs from stakeholders, CONOPS, standards, hazards, interface assumptions, and operational scenarios.
- Separate mission need statements, stakeholder requirements, and system requirements.
- Normalize requirements into atomic, testable statements with stable identifiers.
- Group requirements by hierarchy (system/subsystem/item), functional thread, and lifecycle phase.

#### 1.1 Structuring Rules
- One requirement obligation per statement.
- Include source, rationale, owner, and baseline revision for each requirement.
- Maintain parent-child derivation links and sibling consistency.
- Keep statement text implementation-independent unless implementation is a true constraint.

---

### 2. INCOSE-Aligned Requirement Quality Rules
Apply these quality characteristics to each requirement and flag violations before baselining.

#### 2.1 Required Quality Characteristics
- **Necessary**: expresses a true mission, stakeholder, safety, or regulatory need.
- **Appropriate**: belongs at the current level of abstraction.
- **Unambiguous**: has one reasonable interpretation by independent readers.
- **Complete**: includes needed conditions, units, and limits.
- **Singular (Atomic)**: one main obligation per statement.
- **Feasible**: technically and programmatically achievable.
- **Verifiable**: can be verified by test, analysis, inspection, or demonstration.
- **Correct**: accurately reflects source intent.
- **Conforming**: follows project grammar/style and identifier policy.
- **Traceable**: links to source and downstream artifacts.

#### 2.2 Prohibited / High-Risk Language
Flag and rewrite terms such as: `and/or`, `as appropriate`, `adequate`, `robust`, `user-friendly`, `if possible`, `etc.`, `minimize`, `maximize`, `support`, `optimize`, `quickly`, `normally`.

---

### 3. EARS-Based Requirement Writing and Rewrite
Use EARS patterns as the default syntax framework.

#### 3.1 EARS Patterns
- **Ubiquitous**: `The <system> shall <response>.`
- **Event-driven**: `When <trigger>, the <system> shall <response>.`
- **State-driven**: `While <state>, the <system> shall <response>.`
- **Optional feature**: `Where <feature is present>, the <system> shall <response>.`
- **Unwanted behavior**: `If <fault/abnormal condition>, then the <system> shall <response>.`

#### 3.2 EARS Rewrite Process
1. Classify requirement intent by EARS pattern type.
2. Identify actor/system subject explicitly.
3. Replace vague verbs with measurable outcomes.
4. Add units, thresholds, tolerance, and timing constraints.
5. Confirm single obligation and verification method feasibility.

#### 3.3 Preferred Grammar
- Use **shall** for binding requirements.
- Use **should/may** only outside mandatory requirement statements.
- Keep one main clause; move rationale to metadata, not requirement text.

---

### 4. Ambiguity Detection and Clarification Suggestions
Detect ambiguous language and provide corrected alternatives.

#### 4.1 Ambiguity Triggers
- Subjective qualifiers and non-measurable adjectives.
- Missing units, ranges, tolerances, or timing context.
- Pronouns with unclear antecedents.
- Combined trigger/state/response logic in one unclear sentence.

#### 4.2 Clarification Actions
- Rewrite using appropriate EARS pattern.
- Split compound requirements into separate atomic statements.
- Define measurable pass/fail thresholds.
- Add operating mode and boundary conditions.

---

### 5. Requirements Traceability (Requirements ↔ Design ↔ Verification)
- Build and maintain bi-directional links from each requirement to architecture elements, interfaces, verification artifacts, and hazards/risks when applicable.
- Ensure every requirement has at least one planned verification strategy.
- Detect orphaned requirements and orphaned verification artifacts.

#### 5.1 Minimum Trace Link Set
- Requirement -> Source / Parent requirement
- Requirement -> Allocated component/subsystem
- Requirement -> Interface(s), if applicable
- Requirement -> Verification method and artifact ID(s)
- Requirement -> Hazard/risk link for safety-significant items

---

### 6. Gap and Conflict Detection Across Requirement Sets
- Compare requirements across documents and levels for contradictions and omissions.
- Detect duplicate semantics with different IDs.
- Flag incompatible quantitative limits and conflicting interface assumptions.

#### 6.1 Conflict Types
- Direct contradiction
- Overlapping scope with incompatible constraints
- Derived requirement violating parent intent
- Mode/phase assumptions that conflict across subsystems

#### 6.2 Gap Types
- Missing allocation or ownership
- Missing verification path
- Missing interface boundary behavior
- Missing failure/off-nominal requirements

---

### 7. Resource-Constrained Prioritization and Additional Requirement Suggestions
Create and maintain a prioritized requirement set that reflects limited implementation capacity while preserving mission, safety, and compliance intent.

#### 7.1 Prioritization Dimensions and Scoring
Evaluate each requirement using explicit scoring dimensions:
- Mission/operational value
- Safety/regulatory criticality
- Dependency enablement (unlocks other requirements)
- Risk-reduction impact
- Verification complexity (penalty)
- Implementation effort (penalty)

Use a documented scoring method and keep the rationale per requirement row.

#### 7.2 Priority Tiers (Default)
- **P0 - Mandatory Now**: safety/regulatory/mission-critical requirements that cannot be deferred without formal acceptance.
- **P1 - High Priority**: strong value and near-term feasibility; target current/next baseline.
- **P2 - Planned Backlog**: useful but deferrable with managed impact.
- **P3 - Parking Lot**: low current value or disproportional effort; hold unless trigger condition changes.

#### 7.3 Additional Requirement Suggestion Workflow
- Propose additional requirements discovered through gap/conflict analysis, risk findings, integration issues, or verification shortfalls.
- Label each as `Additional Candidate` until disposition is made.
- For each candidate, provide: problem addressed, expected benefit, affected artifacts, estimated effort, and recommended disposition.

#### 7.4 Disposition States (Accept/Reject/Defer)
- **Accepted**: approved for baseline with owner and target revision.
- **Rejected**: declined with explicit reason and re-entry trigger.
- **Deferred**: not approved now; revisit on stated condition/date.
- **Open**: pending decision.

#### 7.5 Disposition Governance Rules
- No additional candidate may close as Rejected/Deferred without rationale and accountable decision authority.
- No Accepted requirement may enter baseline without downstream impact tags for architecture, V&V, risk/safety, and integration.
- Deferred items must include re-review criteria (date, risk threshold, dependency milestone, or defect trigger).

---

### 8. Natural Language to Formal Specification Conversion
Convert natural language requirements to structured/formal representations without losing intent.

#### 8.1 Supported Representation Forms
- Structured requirement fields: subject, trigger/state, response, constraint, rationale
- Predicate-style logic expressions
- State/event constraints for model-based workflows

#### 8.2 Conversion Rules
- Preserve original text and maintain explicit link to formalized expression.
- Record assumptions and interpretation decisions.
- Require reviewer approval for high-criticality requirements.
- Do not remove the source sentence from controlled records.

---

### 9. Quality & Integrity Rules
- Every requirement must pass INCOSE quality checks before baseline.
- Every requirement should map to an EARS pattern unless a justified exception is documented.
- Every requirement must include owner, source, revision, and trace links.
- Safety/mission-critical requirements must include measurable acceptance limits.
- Requirement wording must support downstream verification planning per IEEE 1012 intent.
- Every requirement in a constrained-delivery baseline must carry a documented priority tier.
- Every additional candidate requirement must carry one disposition state: Open, Accepted, Rejected, or Deferred.

---

## Output Formats

### A. INCOSE + EARS Quality Review Record
```text
| Req ID | Original Text | EARS Pattern | INCOSE Rule Violations | Rewritten Requirement | Verification Method | Reviewer Decision |
|---|---|---|---|---|---|---|
```

### B. Requirement Traceability Extract
```text
| Req ID | Parent/Source | Allocation | Interface Ref | Verification Artifact | Hazard/Risk Ref | Status |
|---|---|---|---|---|---|---|
```

### C. Formalization Record
```text
| Req ID | Natural Language | Structured/EARS Form | Formal Representation | Assumptions | Reviewer Decision |
|---|---|---|---|---|---|
```

### D. EARS Rewrite Worksheet
```text
| Req ID | Pattern Type | Trigger/State/Condition | System Subject | Required Response | Quantitative Constraint | Notes |
|---|---|---|---|---|---|---|
```

### E. Prioritized Requirement Set (Resource-Constrained)
```text
| Req ID | Requirement Statement | Priority Tier (P0-P3) | Value/Criticality Rationale | Effort Estimate | Dependency Impact | Recommended Baseline |
|---|---|---|---|---|---|---|
```

### F. Additional Requirement Disposition Log
```text
| Candidate ID | Suggested Requirement | Source Trigger | Recommendation (Accept/Reject/Defer) | Decision | Decision Rationale | Owner | Revisit Trigger/Date | Downstream Impact Tags (ARC/VNV/RSK/INT) |
|---|---|---|---|---|---|---|---|---|
```

---

## Anti-Patterns

| Anti-Pattern | Violation | Action |
|---|---|---|
| Requirement with ambiguous or subjective wording | Fails unambiguous/verifiable criteria | Rewrite using EARS + measurable constraints |
| Requirement with multiple obligations | Fails atomic/singular criterion | Split into separate requirements |
| Requirement statement using `should`/`may` as mandatory behavior | Weak obligation semantics | Replace with `shall` |
| Requirement with no verification intent | Not verifiable | Add verification method and acceptance criteria |
| Requirement with no trace links | Broken lifecycle traceability | Add source/parent and downstream links |
| Rewritten requirement not linked to original source | Auditability loss | Maintain explicit rewrite linkage |
| Prioritized baseline with un-tiered requirements | Resource planning ambiguity | Assign explicit priority tier and rationale |
| Additional suggestion marked rejected/deferred without rationale | Non-auditable decision process | Record decision authority, reason, and revisit trigger |

---

## Dependencies & Interfaces
- **Depends on:** None
- **Provides to:** SK-ARC-001, SK-VNV-001, SK-RSK-001, SK-INT-001
- **Extended by:** SK-AVN-ADD-001

---

## Changelog

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | [Date] | [Author] | Initial release as consolidated requirements engineering skill. |
| 1.1 | [Date] | [Author] | Added explicit INCOSE-aligned quality characteristics, EARS syntax patterns, rewrite workflow, prohibited language list, and expanded review/output templates for requirements writing and structuring. |
| 1.2 | [Date] | [Author] | Added top-of-document Description section. Added explicit standards integration guidance for ISO/IEC/IEEE 15288, IEEE 1012, and INCOSE SE Handbook. Moved skill to `/skills/generic-skills/`. |
| 1.3 | 2026-03-30 | Cursor Agent | Added resource-constrained requirement prioritization, additional requirement suggestion workflow, explicit Accept/Reject/Defer/Open disposition governance, and new prioritized/disposition output templates. |

---

*Authority: ISO/IEC/IEEE 15288:2023 | IEEE 1012:2016 | INCOSE Systems Engineering Handbook v5 | ISO/IEC/IEEE 29148:2018 | EARS (Mavin/Armstrong)*
