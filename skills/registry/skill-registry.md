# Skill Registry
**Repository:** AI-Enabled Systems Engineering Skill Library
**Maintained by:** Systems Engineering Lead
**Last Updated:** See Git commit history

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
| SK-REQ-003 | Requirements Capture, Traceability & Management | 2.0 | Requirements | General | SK-REQ-001 | SK-REQ-003-AVN | Active | /skills/requirements/requirements-capture-traceability-management-v2.0.md |
| SK-REQ-003-AVN | Requirements Capture, Traceability & Management — Aviation Addendum | 1.0 | Requirements | Aviation | SK-REQ-001, SK-REQ-002, SK-REQ-003, SK-CERT-001 | None | Active | /skills/requirements/requirements-capture-traceability-management-aviation-addendum-v1.0.md |
| SK-REQ-004 | Requirements Field Specification | 1.0 | Requirements | Aviation | SK-REQ-001, SK-REQ-002, SK-REQ-003, SK-REQ-003-AVN | None | Active | /skills/requirements/requirements-field-specification-v1.0.md |
| SK-CERT-001 | Regulatory & Certification Expertise | 1.0 | Certification | Aviation | None | None | Active | /skills/certification/regulatory-certification-expertise-v1.0.md |
| SK-VV-001 | Verification & Validation Planning | 1.0 | Verification | Aviation | SK-REQ-003, SK-REQ-003-AVN, SK-CERT-001 | None | Active | /skills/verification/vv-planning-v1.0.md |
| SK-INTF-001 | Interface Capture & Specification | 2.0 | Interfaces | General | SK-REQ-001, SK-REQ-003 | SK-INTF-001-AVN | Active | /skills/interfaces/interface-capture-specification-v2.0.md |
| SK-INTF-001-AVN | Interface Capture & Specification — Aviation Addendum | 1.0 | Interfaces | Aviation | SK-REQ-001, SK-REQ-002, SK-REQ-003, SK-REQ-003-AVN, SK-INTF-001, SK-CERT-001 | None | Active | /skills/interfaces/interface-capture-specification-aviation-addendum-v1.0.md |
| SK-INTF-002 | Interface Management | 2.0 | Interfaces | General | SK-INTF-001, SK-REQ-003 | SK-INTF-002-AVN | Active | /skills/interfaces/interface-management-v2.0.md |
| SK-INTF-002-AVN | Interface Management — Aviation Addendum | 1.0 | Interfaces | Aviation | SK-INTF-001, SK-INTF-001-AVN, SK-INTF-002, SK-REQ-003, SK-REQ-003-AVN, SK-CERT-001 | None | Active | /skills/interfaces/interface-management-aviation-addendum-v1.0.md |
| SK-DV-001 | Design Values Library | 1.0 | Design Values | General | SK-REQ-001, SK-REQ-003 | None | Active | /skills/design-values/design-values-library-v1.0.md |

---

## Skill Count Summary

| Domain | General | Aviation | Total |
|---|---|---|---|
| Requirements | 2 | 3 | 5 |
| Certification | 0 | 1 | 1 |
| Verification | 0 | 1 | 1 |
| Interfaces | 2 | 4 | 6 |
| Design Values | 1 | 0 | 1 |
| **Total** | **5** | **9** | **14** |

---

## Pending Updates — In Progress

| Skill | Current Scope | Planned Action | Step |
|---|---|---|---|
| SK-VV-001 | Aviation | Generalize base + create SK-VV-001-AVN | Step 5 |

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
| GAP-009 | Requirements Field Specification (General) | Low | Open |
| GAP-010 | General-purpose SK-REQ-003 | Low | **Closed — Step 2** |
| GAP-011 | General-purpose SK-INTF-001 | Low | **Closed — Step 3** |
| GAP-012 | General-purpose SK-INTF-002 | Low | **Closed — Step 4** |
| GAP-013 | General-purpose SK-VV-001 | Low | In Progress — Step 5 |
| GAP-014 | Skill header blocks missing from all skills | Low | **Closed — Step 1** |
