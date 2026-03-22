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
| SK-REQ-003 | Requirements Capture, Traceability & Management | 1.0 | Requirements | Aviation | SK-REQ-001, SK-REQ-002 | None | Active | /skills/requirements/requirements-capture-traceability-management-v1.0.md |
| SK-REQ-004 | Requirements Field Specification | 1.0 | Requirements | Aviation | SK-REQ-001, SK-REQ-002, SK-REQ-003 | None | Active | /skills/requirements/requirements-field-specification-v1.0.md |
| SK-CERT-001 | Regulatory & Certification Expertise | 1.0 | Certification | Aviation | None | None | Active | /skills/certification/regulatory-certification-expertise-v1.0.md |
| SK-VV-001 | Verification & Validation Planning | 1.0 | Verification | Aviation | SK-REQ-003, SK-CERT-001 | None | Active | /skills/verification/vv-planning-v1.0.md |
| SK-INTF-001 | Interface Capture & Specification | 1.0 | Interfaces | Aviation | SK-REQ-001, SK-REQ-002, SK-REQ-003 | None | Active | /skills/interfaces/interface-capture-specification-v1.0.md |
| SK-INTF-002 | Interface Management | 1.0 | Interfaces | Aviation | SK-INTF-001, SK-REQ-003 | None | Active | /skills/interfaces/interface-management-v1.0.md |
| SK-DV-001 | Design Values Library | 1.0 | Design Values | General | SK-REQ-001, SK-REQ-003 | None | Active | /skills/design-values/design-values-library-v1.0.md |

---

## Skill Count Summary

| Domain | General | Aviation | Total |
|---|---|---|---|
| Requirements | 1 | 3 | 4 |
| Certification | 0 | 1 | 1 |
| Verification | 0 | 1 | 1 |
| Interfaces | 0 | 2 | 2 |
| Design Values | 1 | 0 | 1 |
| **Total** | **2** | **7** | **9** |
