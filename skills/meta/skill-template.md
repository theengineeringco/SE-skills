# Skill Template
**Repository:** AI-Enabled Systems Engineering Skill Library
**Purpose:** Standard structure for all new skills. Copy this file, rename it, and populate each section. Do not remove sections — mark them N/A if not applicable.

---

## SKILL HEADER BLOCK
*(Complete this block for every skill. It is read by the registry and dependency map.)*

```
Skill Name:        [Full name matching the registry]
Skill ID:          [SK-[DOMAIN]-[SEQ] — assigned by library owner on merge]
Version:           [1.0 for new skills]
Scope:             [General | Aviation | [other domain]]
Domain:            [Requirements | Certification | Verification | Interfaces | Design Values | MBSE | Safety | Other]
Dependencies:      [Comma-separated Skill IDs, or "None"]
Extended By:       [Comma-separated Skill IDs, or "None" — populated after dependent skills exist]
Status:            [Draft | Active | Deprecated]
Author:            [Name]
Date Created:      [YYYY-MM-DD]
Last Modified:     [YYYY-MM-DD]
Description:       [One sentence — used verbatim in the registry]
```

---

# Skill: [Full Skill Name]

## Role & Purpose
*[2–4 sentences defining what this skill does, what role the model adopts when using it, what program context it applies to, and how it relates to other skills in the library. Be explicit about scope boundaries — what this skill does NOT cover is as important as what it does.]*

---

## Core Competencies

### 1. [First Major Competency Area]
*[Define the first major capability or knowledge domain this skill provides. Each section should be self-contained and actionable — the model should be able to apply it without needing to infer intent.]*

#### 1.1 [Sub-topic if needed]
*[Sub-sections are optional but recommended when a competency area has distinct sub-disciplines.]*

---

### 2. [Second Major Competency Area]
*[Continue for as many sections as needed. Typical skills have 4–10 sections.]*

---

### N. Quality & Integrity Rules
*[Every skill should include at least one section on proactive quality checks, error detection, or integrity rules the model should apply. This is what makes a skill an active reasoning tool rather than a passive knowledge base.]*

---

### N+1. Governance Principles
*[Optional but recommended for skills that manage artifacts, baselines, or program records. State the invariant rules that govern how the skill's outputs are created, maintained, and changed.]*

---

## Output Formats
*[If this skill produces structured outputs (documents, tables, field records, requirement statements), define the format here. Consistent output formats enable downstream skills to consume outputs reliably.]*

```
[Example output structure — use code blocks for structured formats]
```

---

## Anti-Patterns
*[List the failure modes, common errors, or prohibited outputs this skill must detect and flag. Explicit anti-patterns make the skill more robust than implicit quality guidance alone.]*

| Anti-Pattern | Violation | Action |
|---|---|---|
| [Description] | [Why it is wrong] | [What the model should do] |

---

## Dependencies & Interfaces
*[State which skills this skill depends on, what it inherits from them, and what it provides to downstream skills. This section is the prose companion to the dependency map.]*

- **Depends on:** [Skill ID and name — what is inherited or required]
- **Provides to:** [Skill ID and name — what downstream skills consume from this skill]
- **Extends:** [Skill ID and name — if this skill is an addendum or extension, state what it extends and confirm all parent rules remain in force]

---

## Changelog

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | [YYYY-MM-DD] | [Name] | Initial release |

---

*Authority: [Cite governing standards, regulations, or frameworks — e.g., INCOSE GtWR v4, ARP4754A, ISO/IEC/IEEE 29148]*
