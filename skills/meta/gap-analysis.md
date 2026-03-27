# Skill Library — Gap Analysis
**Repository:** AI-Enabled Systems Engineering Skill Library
**Based on:** Consolidated six-skill architecture (SK-REQ-001, SK-ARC-001, SK-VNV-001, SK-RSK-001, SK-INT-001, SK-AVN-ADD-001)
**Version:** 2.0

---

## Current Library Coverage

The current library is intentionally consolidated into five general core skills plus one aviation addendum:

| Discipline | Coverage | Skill |
|---|---|---|
| Requirements engineering | ✅ Strong | SK-REQ-001 |
| Architecture and design | ✅ Strong | SK-ARC-001 |
| Verification and validation | ✅ Strong | SK-VNV-001 |
| Risk and safety analysis | ✅ Strong | SK-RSK-001 |
| Integration and interfaces | ✅ Strong | SK-INT-001 |
| Aviation regulatory overlay (ARP4754A/ARP4761/DO-178C/DO-254) | ✅ Strong | SK-AVN-ADD-001 |

---

## Identified Gaps

### GAP-001 — MBSE Interoperability & Tooling Profiles
**Priority:** Medium
**Trigger:** SK-ARC-001 includes model generation guidance, but repository does not yet define standard exchange profiles, model package conventions, and tool interoperability constraints.
**Proposed Action:** Add a focused section or future companion skill for model interchange profiles, naming conventions, and validation checks.

---

### GAP-002 — Configuration Management (Standalone Discipline)
**Priority:** Medium
**Trigger:** CM concepts are referenced across all skills but not yet treated as a dedicated discipline.
**Proposed Action:** Add a dedicated CM skill or extend core skills with a shared CM control framework and templates.

---

### GAP-003 — Program Planning & Milestone Governance
**Priority:** Medium
**Trigger:** Integration and V&V planning are present, but cross-domain program milestone governance is not explicitly centralized.
**Proposed Action:** Add program-level planning templates for readiness reviews, milestone criteria, and integrated lifecycle dashboarding.

---

## Overlap Analysis

| Overlap | Skills Involved | Assessment | Recommended Action |
|---|---|---|---|
| Safety-related verification content | SK-VNV-001, SK-RSK-001 | Intentional | Keep verification evidence in SK-VNV-001 and risk argument in SK-RSK-001 |
| Interface risk content | SK-INT-001, SK-RSK-001 | Intentional | Maintain explicit cross-links in outputs |
| Aviation objective overlays | SK-AVN-ADD-001 with all core skills | Intentional | Keep aviation content only in SK-AVN-ADD-001 to avoid drift |

---

## Gap Priority Summary

| Priority | Gap IDs | Count |
|---|---|---|
| High | — | 0 |
| Medium | GAP-001, GAP-002, GAP-003 | 3 |
| Low | — | 0 |
| **Total** | | **3** |
