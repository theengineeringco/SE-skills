Skill Name:        SE Tool Data Model Alignment
Skill ID:          SK-META-001
Version:           1.0
Scope:             General
Domain:            Meta
Dependencies:      SK-REQ-003, SK-VV-001, SK-VER-001, SK-INTF-001, SK-INTF-002, SK-DV-001
Extended By:       None
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Defines the canonical systems engineering tool entity model and exact field-level schema used by all skills, including entity names, attribute names, data types, allowed values, and alignment rules.

---

# Skill: SE Tool Data Model Alignment

## Role & Purpose
You are an expert in the systems engineering tool data model. Your function is to enforce one canonical schema across all skill outputs so AI-generated artifacts are directly machine-ingestable without post-processing. This skill is the single source of truth for entity names, field names, data types, allowed values, and required spelling/casing conventions. If any other skill conflicts with this model, this skill takes precedence for tool-integration outputs.

---

## Canonical Entity Model (Authoritative)

### 1) testRun
- `isFolder`: No

| fieldName | dataType | allowedValues |
|---|---|---|
| `name` | string |  |
| `description` | richText |  |
| `status` | enum | `Not Started\|In Progress\|Completed\|Aborted` |
| `environment` | string |  |
| `buildVersion` | string |  |
| `executedBy` | userId |  |

### 2) requirement
- `isFolder`: No

| fieldName | dataType | allowedValues |
|---|---|---|
| `name` | string |  |
| `description` | richText |  |
| `owner` | userId |  |
| `stage` | enum | `Draft\|In Review\|Released` |
| `value` | number |  |
| `unit` | string |  |
| `requirementType` | string |  |
| `dal` | string |  |
| `derived` | enum | `Yes\|No` |
| `derivedRationale` | string |  |
| `verificationMethod` | enumArray | `Test\|Analysis\|Inspection\|Demonstration\|Similarity` |
| `pass/FailCriteria` | string |  |
| `verificationStatus` | enum | `Passed\|Failed\|Pending\|Not Applicable\|In Progress` |
| `independenceRequired` | enum | `Yes\|No` |
| `aiConfidenceScore` | number |  |
| `humanReviewed` | boolean |  |
| `rationale` | string |  |

### 3) testCase
- `isFolder`: No

| fieldName | dataType | allowedValues |
|---|---|---|
| `name` | string |  |
| `description` | richText |  |
| `owner` | userId |  |
| `type` | enum | `Functional\|Performance\|Regression\|Smoke\|Integration\|Safety` |
| `status` | enum | `Draft\|Ready\|Depracated` |
| `priority` | enum | `Critical\|High\|Medium\|Low` |
| `preconditions` | richText |  |
| `steps` | richText |  |
| `expectedResults` | richText |  |
| `postconditions` | richText |  |
| `pass/FailCriteria` | richText |  |

### 4) diagram
- `isFolder`: No

| fieldName | dataType | allowedValues |
|---|---|---|
| `name` | string |  |
| `description` | richText |  |
| `umlText` | richText |  |

### 5) designValue
- `isFolder`: No

| fieldName | dataType | allowedValues |
|---|---|---|
| `name` | string |  |
| `description` | richText |  |
| `value` | number |  |
| `unit` | string |  |
| `sourceReference` | string |  |
| `maturityStage` | enum | `Assumed\|Analyzed\|Tested\|Qualified` |

### 6) system
- `isFolder`: Yes

| fieldName | dataType | allowedValues |
|---|---|---|
| `name` | string |  |
| `description` | richText |  |
| `owner` | userId |  |
| `systemType` | enum | `System\|Subsystem\|Component\|External` |
| `level` | enum | `0 - Program Level\|1 - System Level\|2 - Subsystem Level\|3 - Component Level` |

### 7) document
- `isFolder`: No

| fieldName | dataType | allowedValues |
|---|---|---|
| `name` | string |  |
| `description` | richText |  |
| `owner` | userId |  |

### 8) risk
- `isFolder`: No

| fieldName | dataType | allowedValues |
|---|---|---|
| `name` | string |  |
| `description` | richText |  |
| `failureMode` | richText |  |
| `failureEffect` | richText |  |
| `failureCause` | richText |  |
| `severity` | integer | `1-10` |
| `occurrence` | integer | `1-10` |
| `detection` | integer | `1-10` |
| `mitigation` | richText |  |

### 9) testResults
- `isFolder`: No

| fieldName | dataType | allowedValues |
|---|---|---|
| `name` | string |  |
| `description` | richText |  |
| `status` | enum | `Pass\|Fail\|Blocked\|Skipped` |
| `verdictNotes` | string |  |
| `evidence` | string |  |
| `stepResults` | string |  |
| `notes` | string |  |

### 10) interface
- `isFolder`: No

| fieldName | dataType | allowedValues |
|---|---|---|
| `name` | string |  |
| `description` | richText |  |
| `provider` | string |  |
| `consumer` | string |  |
| `interfaceType` | string |  |
| `direction` | string |  |
| `protocol/Standard` | string |  |
| `status` | enum | `Draft\|Approved\|Depracated` |
| `ai-generated` | enum | `Yes\|No` |
| `aiConfidenceScore` | number | `<=1` |
| `humanReviewed` | boolean |  |
| `owner` | userId |  |

### 11) testPlan
- `isFolder`: No

| fieldName | dataType | allowedValues |
|---|---|---|
| `name` | string |  |
| `description` | richText |  |
| `objectives` | richText |  |
| `scope` | richText |  |
| `approach` | richText |  |
| `verificationLevel` | richText |  |
| `entryCriteria` | richText |  |
| `exitCriteria` | richText |  |
| `equipmentRequired` | richText |  |
| `facilitiesRequired` | richText |  |
| `personnelRequired` | richText |  |
| `assumptionsOrConstraints` | richText |  |

### 12) feature
- `isFolder`: No

| fieldName | dataType | allowedValues |
|---|---|---|
| `name` | string |  |
| `description` | richText |  |

### 13) designValueFolder
- `isFolder`: Yes

| fieldName | dataType | allowedValues |
|---|---|---|
| `name` | string |  |
| `description` | richText |  |

### 14) function
- `isFolder`: No

| fieldName | dataType | allowedValues |
|---|---|---|
| `name` | string |  |
| `description` | richText |  |

### 15) useCase
- `isFolder`: No

| fieldName | dataType | allowedValues |
|---|---|---|
| `name` | string |  |
| `description` | richText |  |

### 16) requirementsGroup
- `isFolder`: Yes

| fieldName | dataType | allowedValues |
|---|---|---|
| `name` | string |  |
| `description` | richText |  |

---

## Cross-Entity Alignment Rules

1. **Exact field names are mandatory.** Preserve punctuation and case exactly, including:
   - `pass/FailCriteria`
   - `protocol/Standard`
   - `ai-generated`
   - `testResults`

2. **Enum values are mandatory and closed sets.**
   - Do not substitute synonyms (for example, `Deprecated` is invalid where `Depracated` is the schema value).
   - `verificationStatus` on `requirement` must use only:
     - `Passed`, `Failed`, `Pending`, `Not Applicable`, `In Progress`.

3. **Skill outputs must be schema-first.**
   - All narrative skill guidance must map back to these entity fields.
   - If extra analytic fields are needed, place them in narrative context, not as canonical entity attributes.

4. **Folder semantics**
   - Entities marked `isFolder = Yes` are structural grouping nodes and should not be treated as executable verification records.

5. **AI provenance fields**
   - Where available (`requirement`, `interface`), both `aiConfidenceScore` and `humanReviewed` should be considered before workflow closure.

---

## Anti-Patterns

| Anti-Pattern | Violation | Action |
|---|---|---|
| Using `Deprecated` instead of `Depracated` on model outputs | Schema mismatch to tool enum | Emit exact schema enum value `Depracated` |
| Using `pass_fail_criteria` or `passFailCriteria` | Field name mismatch | Use exact field `pass/FailCriteria` |
| Using `protocolStandard` | Field name mismatch | Use exact field `protocol/Standard` |
| Using `aiGenerated` | Field name mismatch | Use exact field `ai-generated` |
| Requirement verification statuses like `Open/Closed/Verified` | Enum mismatch | Map to `Passed/Failed/Pending/Not Applicable/In Progress` |

---

## Dependencies & Interfaces

- **Depends on:** SK-REQ-003, SK-VV-001, SK-VER-001, SK-INTF-001, SK-INTF-002, SK-DV-001
- **Provides to:** All skill documents that emit structured tool-ready artifacts

---

## Changelog

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | [Date] | [Author] | Initial release. Added canonical entity/field/type/enum schema aligned to the systems engineering tool data model. |

---

*Authority: Program-defined SE Tool Data Model (entityType/isFolder/fieldName/dataType/allowedValues)*
