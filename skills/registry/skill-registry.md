Skill Name:        Skill Registry
Version:           1.4
Last Updated:      2026-03-27
Maintained by:     Systems Engineering Lead

---

# Skill Registry
**Repository:** AI-Enabled Systems Engineering Skill Library

---

## Registry Format

| Field | Description |
|---|---|
| ID | Unique skill identifier. Format: SK-[domain prefix]-[sequence] |
| Name | Full skill name |
| Version | Current approved version (Major.Minor) |
| Domain | Primary engineering domain |
| Scope | General (any program) or Aviation (FAA certification programs) |
| Dependencies | Skill IDs this skill explicitly extends or requires |
| Extended By | Skill IDs that extend or depend on this skill |
| Status | Active / Draft / Deprecated |
| File | Path to skill file in repository |
| Description | One-sentence description |

---

## Skill Index

| ID | Name | Version | Domain | Scope | Dependencies | Extended By | Status | File |
|---|---|---|---|---|---|---|---|---|
| SK-REQ-001 | Requirements Writing | 2.1 | Requirements | General | None | SK-REQ-002 | Active | /skills/requirements/requirements-writing-skill-v2.1.md |
| SK-REQ-002 | Requirements Writing — Aviation Certification Addendum | 1.0 | Requirements | Aviation | SK-REQ-001 | None | Active | /skills/requirements/requirements-writing-aviation-addendum-v1.0.md |
| SK-REQ-003 | Requirements Capture, Traceability & Management | 2.1 | Requirements | General | SK-REQ-001 | SK-REQ-003-AVN | Active | /skills/requirements/requirements-capture-traceability-management-v2.1.md |
| SK-REQ-003-AVN | Requirements Capture, Traceability & Management — Aviation Addendum | 1.0 | Requirements | Aviation | SK-REQ-001, SK-REQ-002, SK-REQ-003, SK-CERT-001 | None | Active | /skills/requirements/requirements-capture-traceability-management-aviation-addendum-v1.0.md |
| SK-REQ-004 | Requirements Field Specification | 1.1 | Requirements | General | SK-REQ-001, SK-REQ-003, SK-VV-001, SK-DM-001 | None | Active | /skills/requirements/requirements-field-specification-v1.0.md |
| SK-DM-001 | SE Tool Data Model | 1.0 | Meta | General | None | SK-REQ-004, SK-VV-001, SK-VER-001, SK-INTF-001, SK-INTF-002, SK-DV-001 | Active | /skills/meta/se-tool-data-model-skill-v1.0.md |
| SK-CERT-001 | Regulatory & Certification Expertise | 1.0 | Certification | Aviation | None | None | Active | /skills/certification/regulatory-certification-expertise-v1.0.md |
| SK-VV-001 | Verification & Validation Planning | 2.2 | Verification | General | SK-REQ-003, SK-DM-001 | SK-VV-001-AVN | Active | /skills/verification/vv-planning-v2.1.md |
| SK-VV-001-AVN | Verification & Validation Planning — Aviation Addendum | 1.1 | Verification | Aviation | SK-REQ-003, SK-REQ-003-AVN, SK-VV-001, SK-CERT-001 | SK-VER-001-AVN | Active | /skills/verification/vv-planning-aviation-addendum-v1.1.md |
| SK-VER-001 | Verification | 1.3 | Verification | General | SK-REQ-003, SK-VV-001, SK-DV-001, SK-DM-001 | SK-VER-001-AVN | Active | /skills/verification/verification-v1.2.md |
| SK-VCRM-001 | Verification Cross-Reference Matrix (VCRM) Authoring & Coverage Assessment | 1.0 | Verification | General | SK-REQ-003, SK-VV-001, SK-VER-001, SK-DM-001 | None | Active | /skills/verification/verification-cross-reference-matrix-v1.0.md |
| SK-VER-001-AVN | Verification — Aviation Addendum | 1.2 | Verification | Aviation | SK-REQ-003, SK-REQ-003-AVN, SK-VV-001, SK-VV-001-AVN, SK-VER-001, SK-CERT-001 | None | Active | /skills/verification/verification-aviation-addendum-v1.2.md |
| SK-INTF-001 | Interface Capture & Specification | 2.1 | Interfaces | General | SK-REQ-001, SK-REQ-003, SK-DM-001 | SK-INTF-001-AVN | Active | /skills/interfaces/interface-capture-specification-v2.0.md |
| SK-INTF-001-AVN | Interface Capture & Specification — Aviation Addendum | 1.0 | Interfaces | Aviation | SK-REQ-001, SK-REQ-002, SK-REQ-003, SK-REQ-003-AVN, SK-INTF-001, SK-CERT-001 | None | Active | /skills/interfaces/interface-capture-specification-aviation-addendum-v1.0.md |
| SK-INTF-002 | Interface Management | 2.2 | Interfaces | General | SK-INTF-001, SK-REQ-003, SK-DM-001 | SK-INTF-002-AVN | Active | /skills/interfaces/interface-management-v2.1.md |
| SK-INTF-002-AVN | Interface Management — Aviation Addendum | 1.0 | Interfaces | Aviation | SK-INTF-001, SK-INTF-001-AVN, SK-INTF-002, SK-REQ-003, SK-REQ-003-AVN, SK-CERT-001 | None | Active | /skills/interfaces/interface-management-aviation-addendum-v1.0.md |
| SK-DV-001 | Design Values Library | 1.2 | Design Values | General | SK-REQ-001, SK-REQ-003, SK-DM-001 | SK-VER-001 | Active | /skills/design-values/design-values-library-v1.0.md |

---

## Skill Count Summary

| Domain | General | Aviation | Total |
|---|---|---|---|
| Requirements | 3 | 2 | 5 |
| Certification | 0 | 1 | 1 |
| Verification | 3 | 2 | 5 |
| Interfaces | 2 | 2 | 4 |
| Design Values | 1 | 0 | 1 |
| Meta | 1 | 0 | 1 |
| **Total** | **10** | **7** | **17** |

---

## Pending Updates

| Item | Description | Action Required |
|---|---|---|
| None | No pending registry consistency updates at this time. | None |

---

## Gap Analysis Summary

| Gap ID | Description | Priority | Status |
|---|---|---|---|
| GAP-001 | MBSE / SysML Modeling Skill | High | Open |
| GAP-002 | System Safety Assessment Skill | High | Open |
| GAP-003 | Software Development Assurance (DO-178C) | Medium | Open |
| GAP-004 | Hardware Development Assurance (DO-254) | Medium | Open |
| GAP-005 | Trade Study & Architecture Decision Records | Medium | Open |
| GAP-006 | Configuration Management | Medium | Open |
| GAP-007 | Means of Compliance Documentation | Medium | Open |
| GAP-008 | Human Factors & Crew Interface | Low–Medium | Open |
| GAP-009 | Requirements Field Specification (General) | Low | **Closed — 2026-03-24** |
| GAP-010 | General-purpose SK-REQ-003 | Low | **Closed — Step 2** |
| GAP-011 | General-purpose SK-INTF-001 | Low | **Closed — Step 3** |
| GAP-012 | General-purpose SK-INTF-002 | Low | **Closed — Step 4** |
| GAP-013 | General-purpose SK-VV-001 | Low | **Closed — Step 5** |
| GAP-014 | Skill header blocks missing from all skills | Low | **Closed — Step 1** |
| GAP-015 | Verification data model skill (SK-VER-001) | Medium | **Closed — 2026-03-22** |
| GAP-016 | Canonical SE tool data model skill | High | **Closed — 2026-03-24** |

---

## Dependency Map Summary

The following diagram shows the dependency relationships between all active skills. Arrows indicate "depends on" direction.

```
SK-CERT-001
  ├──► SK-REQ-003-AVN
  ├──► SK-VV-001-AVN
  ├──► SK-VER-001-AVN
  ├──► SK-INTF-001-AVN
  └──► SK-INTF-002-AVN

SK-REQ-001
  ├──► SK-REQ-002
  ├──► SK-REQ-003
  ├──► SK-REQ-004
  ├──► SK-INTF-001
  └──► SK-DV-001

SK-REQ-003
  ├──► SK-REQ-003-AVN
  ├──► SK-REQ-004
  ├──► SK-VV-001
  ├──► SK-VER-001
  ├──► SK-VCRM-001
  ├──► SK-INTF-001
  ├──► SK-INTF-002
  └──► SK-DV-001

SK-DM-001
  ├──► SK-REQ-004
  ├──► SK-VV-001
  ├──► SK-VER-001
  ├──► SK-VCRM-001
  ├──► SK-INTF-001
  ├──► SK-INTF-002
  └──► SK-DV-001

SK-VV-001
  ├──► SK-REQ-004
  ├──► SK-VCRM-001
  ├──► SK-VV-001-AVN
  └──► SK-VER-001

SK-VER-001 ──► SK-VCRM-001

SK-VV-001-AVN ──► SK-VER-001-AVN
SK-VER-001 ──► SK-VER-001-AVN
SK-INTF-001 ──► SK-INTF-001-AVN
SK-INTF-002 ──► SK-INTF-002-AVN
```
