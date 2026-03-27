Skill Name:        Skill Registry
Version:           2.1
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
| Scope | General or Aviation |
| Dependencies | Skill IDs this skill depends on |
| Extended By | Skill IDs that extend this skill |
| Status | Active / Draft / Deprecated |
| File | Path to skill file in repository |
| Description | One-sentence description |

---

## Skill Index

| ID | Name | Version | Domain | Scope | Dependencies | Extended By | Status | File |
|---|---|---|---|---|---|---|---|---|
| SK-REQ-001 | Requirements Engineering | 1.1 | Requirements | General | None | SK-AVN-ADD-001 | Active | /skills/requirements/requirements-engineering-v1.1.md |
| SK-ARC-001 | Architecture & Design | 1.0 | Architecture | General | SK-REQ-001 | SK-AVN-ADD-001 | Active | /skills/architecture/architecture-and-design-v1.0.md |
| SK-VNV-001 | Verification & Validation | 1.0 | Verification | General | SK-REQ-001, SK-ARC-001 | SK-AVN-ADD-001 | Active | /skills/verification/verification-and-validation-v1.0.md |
| SK-RSK-001 | Risk & Safety Analysis | 1.0 | Safety | General | SK-REQ-001, SK-ARC-001, SK-VNV-001 | SK-AVN-ADD-001 | Active | /skills/safety/risk-and-safety-analysis-v1.0.md |
| SK-INT-001 | Integration & Interfaces | 1.0 | Integration | General | SK-REQ-001, SK-ARC-001, SK-VNV-001, SK-RSK-001 | SK-AVN-ADD-001 | Active | /skills/integration/integration-and-interfaces-v1.0.md |
| SK-AVN-ADD-001 | Aviation Systems Engineering Addendum | 1.0 | Addendum | Aviation | SK-REQ-001, SK-ARC-001, SK-VNV-001, SK-RSK-001, SK-INT-001 | None | Active | /skills/aviation/aviation-systems-engineering-addendum-v1.0.md |

---

## Skill Count Summary

| Domain | General | Aviation | Total |
|---|---|---|---|
| Requirements | 1 | 0 | 1 |
| Architecture | 1 | 0 | 1 |
| Verification | 1 | 0 | 1 |
| Safety | 1 | 0 | 1 |
| Integration | 1 | 0 | 1 |
| Addendum | 0 | 1 | 1 |
| **Total** | **5** | **1** | **6** |

---

## Pending Updates

| Item | Description | Action Required |
|---|---|---|
| None | Registry reflects consolidated six-skill structure. | None |

---

## Gap Analysis Summary

| Gap ID | Description | Priority | Status |
|---|---|---|---|
| GAP-001 | MBSE model interoperability profiles/tooling conventions depth | Medium | Open |
| GAP-002 | Configuration management as standalone skill | Medium | Open |
| GAP-003 | Program planning and milestone orchestration skill | Medium | Open |

---

## Dependency Map Summary

The following diagram shows dependency relationships for the consolidated skill model.

```text
SK-REQ-001
  ├──► SK-ARC-001
  ├──► SK-VNV-001
  ├──► SK-RSK-001
  └──► SK-INT-001

SK-ARC-001 ──► SK-VNV-001
SK-ARC-001 ──► SK-RSK-001
SK-ARC-001 ──► SK-INT-001

SK-VNV-001 ──► SK-RSK-001
SK-VNV-001 ──► SK-INT-001

SK-RSK-001 ──► SK-INT-001

SK-REQ-001
SK-ARC-001
SK-VNV-001
SK-RSK-001
SK-INT-001
  └──► SK-AVN-ADD-001 (aviation overlay)
```
