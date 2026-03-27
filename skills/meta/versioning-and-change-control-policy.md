# Skill Library — Versioning & Change Control Policy
**Repository:** AI-Enabled Systems Engineering Skill Library
**Version:** 1.0

---

## 1. Version Numbering

All skills use a **Major.Minor** version number.

| Increment | When to Use | Examples |
|---|---|---|
| **Major (X.0)** | Structural changes: new sections added, sections removed, governing authority changed, scope changed, dependency added or removed | v1.0 → v2.0 |
| **Minor (x.Y)** | Content changes within existing structure: rules clarified, examples added, anti-patterns added, terminology aligned with another skill | v1.0 → v1.1 |

**Rules:**
- Version numbers never decrement.
- A skill at Draft status uses version 0.x until first approval.
- The registry must reflect the current approved version at all times.
- The filename includes the version number (e.g., `requirements-engineering-v1.0.md`). On version change, the old file is retained in Git history — do not delete it.

---

## 2. Change Initiation

Changes to skills may be initiated by:
- **Gap identified in use** — a skill fails to cover a scenario encountered in practice
- **New standard or regulation** — a governing authority document is revised
- **Dependency change** — an upstream skill changes and requires downstream review
- **Overlap identified** — a library review identifies duplicated content between skills
- **New skill addition** — a new skill implies updates to existing skills' "Extended By" fields and dependency maps

All changes are initiated via a **Skill Change Request (SCR)** recorded in the repository's issue tracker or equivalent, containing:
- Skill ID and current version
- Description of the proposed change
- Reason / trigger
- Impact assessment: list of dependent skills requiring review
- Proposed new version number

---

## 3. Change Control by Change Type

### Minor Changes (x.Y)
1. Author drafts the change in a feature branch
2. At least one peer reviewer confirms the change does not alter scope or break dependencies
3. Changelog section updated in the skill file
4. Registry updated to new version number
5. Merged to main branch

### Major Changes (X.0)
1. SCR approved by library owner before work begins
2. Author drafts the change in a feature branch
3. All dependent skills reviewed for compatibility (per impact analysis table in dependency map)
4. Dependent skills updated in the same pull request if required
5. Changelog section updated in the skill file
6. Registry, dependency map, and gap analysis updated
7. Two reviewers required before merge
8. Merged to main branch with a tagged release

### New Skill Addition
1. Author uses the skill template to draft the new skill
2. Skill header block completed in full
3. Registry entry added
4. Dependency map updated
5. Gap analysis updated to mark addressed gaps
6. One reviewer confirms the skill does not duplicate existing content
7. Merged to main branch

### Skill Deprecation
1. Status set to Deprecated in registry
2. Deprecated notice added to top of skill file with date and reason
3. Any skills that depended on the deprecated skill are updated to remove or replace the dependency
4. Skill file retained in repository — never deleted

---

## 4. Branching Convention

| Branch | Purpose |
|---|---|
| `main` | Approved, active skills only. All skills on main are considered production-ready. |
| `draft/[skill-id]-[description]` | New skill drafts under development |
| `update/[skill-id]-v[version]` | Updates to existing skills |
| `review/library-[date]` | Periodic library-level gap and overlap review branches |

---

## 5. Periodic Library Review

Conduct a full library review on the following triggers:
- **Scheduled:** Every 6 months, or at each major program milestone
- **Event-driven:** When 3 or more skills have been updated since the last review, or when a new governing standard is released

**Library review scope:**
1. Registry accuracy — confirm all skill IDs, versions, dependencies, and statuses are current
2. Dependency map accuracy — confirm all dependency relationships reflect current skill content
3. Gap analysis update — identify new gaps implied by program evolution or skill changes
4. Overlap analysis — identify any content duplicated across skills and resolve
5. Terminology consistency — confirm that key terms (DAL, requirement level, verification method, etc.) are used consistently across all skills
6. New skill candidates — identify gaps that warrant new skill development

Library review outputs are committed to the `review/library-[date]` branch and merged to main after approval.

---

## 6. AI Session Usage Protocol

When loading skills into an AI tool session for review or use:

1. **Always load the registry first.** The registry gives the AI the full library context before any individual skill is analyzed.
2. **Load the dependency map second** when conducting library-level analysis, gap review, or skill improvement sessions.
3. **Load individual skill files** as needed for detailed review, improvement, or use.
4. **State the session intent explicitly:** "Review SK-INT-001 for gaps" produces a different analysis than "Use SK-INT-001 to capture interfaces for the propulsion system." The AI should be told which mode it is operating in.
5. **Output from AI review sessions** (gap findings, overlap findings, improvement suggestions) should be captured as SCRs before the session ends — AI session outputs are not automatically committed to the repository.
