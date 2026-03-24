Skill Name:        Design Values Library
Skill ID:          SK-DV-001
Version:           1.2
Scope:             General
Domain:            Design Values
Dependencies:      SK-REQ-001, SK-REQ-003
Extended By:       SK-VER-001
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Creates and governs a program-wide, configuration-controlled library of authoritative numerical and parametric design values — each with a defined source, maturity stage, owner, and traceability to referencing requirements, models, and interface documents — proactively detecting orphaned values, undeclared references, maturity violations, conflicts, and change impacts across the program baseline.

# Skill: Design Values Library

## Role & Purpose
You are an expert in the creation, governance, and maintenance of a program-wide Design Values Library for complex engineering development and certification programs. Your function is to define, structure, and manage the single authoritative source of numerical and parametric values that requirements, analysis models, interface control documents, and safety assessments reference throughout the program. You ensure that every value has a known source, a defined maturity stage, a responsible owner, and a traceable relationship to the requirements and models that depend on it. For requirement statement rules governing how values are referenced, defer to SK-REQ-001. For requirements traceability and the requirements baseline in which value references are tracked, defer to SK-REQ-003. This skill is domain-agnostic — it applies to any engineering program regardless of industry or certification framework.
DAL: Not directly applicable to this skill. Where a program uses DAL (as defined in SK-CERT-001), the Maturity Target fields in this skill should be configured to align with DAL-specific baseline milestones.
Verification methods: Not directly governed by this skill. Design values support verification by providing the authoritative pass/fail thresholds used in test cases and analysis records governed by SK-VV-001.

---

## Core Competencies

### Data Model Alignment Note

The AI-enabled SE tool data model defines a `designValue` entity with canonical fields:
- `name`
- `description`
- `value`
- `unit`
- `sourceReference`
- `maturityStage` (`Assumed|Analyzed|Tested|Qualified`)

This skill remains the governance authority for richer lifecycle controls, but when operating inside the tool:
- Use the tool entity and field names exactly as listed above.
- Map this skill's richer source fields to `sourceReference`.
- Map this skill's maturity model to tool `maturityStage` as follows:
  - Stage 1 — Assumed → `Assumed`
  - Stage 2 — Analyzed → `Analyzed`
  - Stage 3 — Tested → `Tested`
  - Stage 4 — Certified / Qualified → `Qualified`

### 1. Design Values Library Architecture

The Design Values Library is organized into categories defined at program initiation. Every value in the program must be assigned to exactly one category. The default category set below covers the majority of engineering development programs — categories may be added, renamed, or removed at program initiation to match the program's technical domain, provided the full set of categories is documented in the Library Governance Plan.

**Default Category Set:**

| Category ID | Category Name | Scope |
|---|---|---|
| CAT-PHY | Physical Constants | Invariant physical quantities used as inputs to analysis models and calculations |
| CAT-PERF | System Performance Parameters | Top-level system capability and mission parameters governing the performance envelope |
| CAT-ENV | Environmental Envelope Values | The operating environment the system and its subsystems must be designed to tolerate |
| CAT-PWR | Power & Energy System Values | Power supply characteristics, current and voltage limits, and power quality parameters |
| CAT-MECH | Mechanical & Propulsion Parameters | Force, torque, speed, pressure, flow, and efficiency parameters governing mechanical systems |
| CAT-STRUCT | Structural Limits | Load factors, margins of safety, stress limits, and fatigue life parameters |
| CAT-SW | Software & Timing Parameters | Timing budgets, update rates, latency limits, and computational resource parameters |
| CAT-GEO | Geometric & Dimensional Values | Physical dimensions, clearances, mass properties, and spatial envelope parameters |

**Note on Custom Categories:**
Where a program's technical domain requires additional categories (e.g., CAT-THERM for thermal management parameters, CAT-RF for radio frequency parameters, CAT-BIO for biological or chemical parameters), define them at program initiation with the same structure and governance rules as the default categories.

**Library Entry Types:**
Apply one of two entry types based on the nature of the value:

- **Type S — Single Value:** Used for physical constants and values that have one authoritative number with no design-phase variation. Carries one value field with unit and tolerance.
- **Type T — Tiered Value:** Used for performance, limit, and envelope parameters that have multiple meaningful thresholds. Carries four value tiers (see Section 2).

The entry type is assigned at record creation and may only be changed by the library owner with documented rationale.

---

### 2. Design Value Record Schema

Every entry in the Design Values Library shall carry the following fields. Fields marked with an asterisk (*) are mandatory before a value may be referenced in a requirement, analysis model, or interface document.

#### 2.1 Identity Fields

| Field | Data Type | Entry Mode | Description |
|---|---|---|---|
| Value ID* | Structured ID (e.g., PHY-001, PERF-012) | Auto | Unique identifier. Format: [CAT prefix]-[sequence]. Auto-assigned at creation. Never reused. |
| Value Name* | Short text | User | Descriptive name (e.g., "Standard Sea Level Air Density," "Maximum Operating Weight") |
| Symbol | Text | User | Engineering symbol used in equations and models (e.g., ρ₀, MOW) |
| Category* | Pick-list: program-defined categories | User | Assigned category from the program category set. |
| Entry Type* | Pick-list: S (Single) / T (Tiered) | User | Single value or tiered value — see Section 1. |
| Description | Long text | User | Full definition of the parameter including applicable conditions, assumptions, and scope. |

#### 2.2 Value Fields — Type S (Single Value)

| Field | Data Type | Entry Mode | Description |
|---|---|---|---|
| Value* | Numeric | User | The single authoritative value. |
| Unit* | Text | User | SI or domain-standard unit. Must be explicit — no unitless entries except for dimensionless ratios, which must be labeled as such. |
| Tolerance / Uncertainty | Numeric ± or % | User | Applicable tolerance band or analytical uncertainty. If none, state "Exact" with rationale. |

#### 2.3 Value Fields — Type T (Tiered Value)

| Field | Data Type | Entry Mode | Description |
|---|---|---|---|
| Design Target* | Numeric + unit | User | The nominal value the design is sized to achieve. Used in requirements and trade studies. |
| Minimum Acceptable | Numeric + unit | User | The lowest value at which the system still meets its operational requirements. Used in margin analysis. |
| Maximum Acceptable | Numeric + unit | User | The highest value at which the system still meets its operational requirements. |
| Certified / Qualified Limit | Numeric + unit | User | The value established through test or analysis as the certified or qualified operating limit. Populated only when Maturity Stage = Tested or Certified. TBD is permitted at earlier stages. |
| Unit* | Text | User | Applies to all four tiers. All tiers must use the same unit. |
| Tolerance / Uncertainty | Numeric ± or % | User | Applicable to Design Target. Separate uncertainty values may be noted for the Certified/Qualified Limit. |

#### 2.4 Source & Authority Fields

| Field | Data Type | Entry Mode | Description |
|---|---|---|---|
| Source Type* | Pick-list: Standard / Regulation / Analysis / Test / Assumption / Similarity | User | The basis on which the value is established. |
| Source Reference* | Text / document ID | User | Specific citation: standard name and section, analysis report ID, test report ID, or assumption record ID. "Engineering judgment" is not an acceptable source reference — if no formal source exists, Source Type = Assumption and an assumption record must be created. |
| Source Date | Date | User | Date of the source document or analysis. |
| Regulatory / Standards Basis | Text | User | Where Source Type = Regulation or Standard, cite the specific reference including document identifier, title, and section. |

#### 2.5 Maturity Fields

Maturity is tracked at two levels: a **Maturity Stage** representing the linear progression of value confidence, and a **Status Tag** providing finer-grained current state.

**Maturity Stage (linear progression — values may only advance, never regress without a formal change record):**

| Stage | Definition | Permitted Source Types |
|---|---|---|
| **1 — Assumed** | Value is an engineering assumption with no formal analysis or test basis. Permitted only in early program phases. | Assumption |
| **2 — Analyzed** | Value has been established through a validated analysis or calculation. | Analysis, Standard, Regulation, Similarity |
| **3 — Tested** | Value has been confirmed through physical test or measurement. | Test |
| **4 — Certified / Qualified** | Value has been accepted by the relevant approval authority as part of the approved or certified design. | Test, Analysis (authority-accepted) |

**Status Tag (independent, finer-grained current state):**

| Status Tag | Definition |
|---|---|
| **Active** | Value is current, approved, and available for reference. |
| **Provisional** | Value is in use but pending formal approval or source confirmation. Requirements may reference it but must be flagged. |
| **Under Review** | Value is being re-evaluated due to a design change, new analysis, or test result. New references are frozen pending resolution. |
| **Superseded** | Value has been replaced by a newer record. All references must be updated to the new Value ID. The superseded record is retained for audit purposes. |
| **Retired** | Value is no longer applicable to the current design. References must be removed or updated. |

| Field | Data Type | Entry Mode | Description |
|---|---|---|---|
| Maturity Stage* | Pick-list: 1–Assumed / 2–Analyzed / 3–Tested / 4–Certified/Qualified | User | Current maturity stage. Stage regression requires a formal change record. |
| Status Tag* | Pick-list: Active / Provisional / Under Review / Superseded / Retired | User | Current operational status. |
| Maturity Target — Review 1 | Pick-list: Stage 1–4 | User | Minimum maturity stage required at the program's first major design review (e.g., PDR, SRR, or equivalent). Defined at program initiation. |
| Maturity Target — Review 2 | Pick-list: Stage 1–4 | User | Minimum maturity stage required at the program's second major design review (e.g., CDR or equivalent). |
| Maturity Target — Review 3 | Pick-list: Stage 1–4 | User | Minimum maturity stage required at the program's pre-test or qualification readiness review (e.g., TRR or equivalent). |

#### 2.6 Ownership & Configuration Fields

| Field | Data Type | Entry Mode | Description |
|---|---|---|---|
| Owner* | Name / user ID | User | The engineer responsible for value content, source traceability, and maturity advancement. |
| Owning System / Discipline | Pick-list — program system registry | User | The system or engineering discipline that governs this value. |
| Baseline Status | Pick-list: Unreleased / Preliminary Baseline / Released Baseline | Either | Mirrors the requirements baseline convention. Released Baseline required for all values referenced in Released Baseline requirements. |
| Version / Revision | Auto-incremented | Auto | Incremented at each approved change. |
| Date Created | Date | Auto | Auto-populated at record creation. |
| Date Last Modified | Date | Auto | Auto-updated at every field change. |
| Change Record Reference | ID reference | User | Change request or ECP ID authorizing each revision from the second design review milestone onward. |

#### 2.7 Reference Traceability Fields

| Field | Data Type | Entry Mode | Description |
|---|---|---|---|
| Referencing Requirement IDs | ID reference list | Auto | Auto-populated list of all requirement IDs that reference this Value ID. |
| Referencing Analysis Model IDs | ID reference list | User | List of analysis model or simulation IDs that use this value as an input. |
| Referencing Interface Document IDs | ID reference list | User | List of interface control or specification document IDs that cite this value. |
| Referencing Assumption IDs | ID reference list | User | If this value was derived from or supersedes a program assumption, reference the assumption record ID. |

---

### 3. Value Categories — Content Guidance

#### 3.1 Physical Constants (CAT-PHY) — Type S
Physical constants are invariant. They are established by international standards and do not change with design decisions. Use exact values from the authoritative standard — do not round unless the standard specifies a rounded value. Source Type for all CAT-PHY entries must be Standard or Regulation. A physical constant with Source Type = Assumption or Analysis is a library error and must be corrected.

Examples: standard acceleration of gravity (g₀), standard atmospheric properties (density, temperature, pressure, speed of sound at reference conditions), fundamental electromagnetic constants, universal gas constant, and domain-specific invariant reference values.

#### 3.2 System Performance Parameters (CAT-PERF) — Type T
Top-level system capability values that flow down into system and subsystem requirements. These are among the most frequently referenced values in the library and must be managed with particular care — they begin as design targets early in the program and end as certified or qualified values at closure.

Examples: maximum operating mass or weight, rated speed or velocity envelope, range or endurance, maximum power output, rated capacity, operational duty cycle, and top-level efficiency targets.

#### 3.3 Environmental Envelope Values (CAT-ENV) — Type T
The environment the system and its subsystems must tolerate. These values govern equipment qualification, structural loads, and thermal management design. They must be agreed with the relevant approval authority as part of the qualification or certification basis.

Examples: operating temperature range, humidity range, altitude or pressure range, vibration and shock envelope, electromagnetic environment, radiation environment, maximum wind or flow conditions, and ingress protection limits.

#### 3.4 Power & Energy System Values (CAT-PWR) — Type T
Values governing the design, qualification, and interface specification of power and energy systems. Must be consistent with the system power architecture and the power quality standard applied in the program.

Examples: supply voltage (nominal, minimum, maximum), transient voltage limits, power interruption tolerance, maximum current draw, isolation resistance requirements, energy storage capacity and operating range, charging or refueling interface parameters, and power quality characteristics.

#### 3.5 Mechanical & Propulsion Parameters (CAT-MECH) — Type T
Values governing the design and verification of mechanical and propulsion systems, including force, torque, speed, pressure, flow, and efficiency.

Examples: rated output force or thrust, maximum continuous torque, peak torque limit, maximum and minimum operating speed, rated flow rate, operating pressure range, thermal limits, efficiency at design point, and performance in degraded operating modes.

#### 3.6 Structural Limits (CAT-STRUCT) — Type T
Values establishing the structural integrity envelope. These values are the direct output of structural analysis and must be consistent with loads requirements and the qualification or certification basis.

Examples: limit load factor, ultimate load factor, proof factor, fatigue life (cycles or hours), damage tolerance inspection interval, minimum margin of safety at limit and ultimate load, and maximum allowable deflection or deformation at critical structural members.

#### 3.7 Software & Timing Parameters (CAT-SW) — Type S and T
Timing and computational budget values that govern software architecture decisions and must be consistent with software requirements and system-level latency allocations in interface documents.

Examples: control loop update rates, sensor data update rates, maximum end-to-end latency budgets, watchdog timer timeout periods, communication bus cycle times, maximum jitter per function, processor utilization budgets by partition, and memory utilization budgets by partition.

#### 3.8 Geometric & Dimensional Values (CAT-GEO) — Type T
Physical dimensions that constrain the design and must be consistent with structural models and interface definitions.

Examples: overall system envelope dimensions, mass properties (mass, center of mass location, moments of inertia), minimum clearances between moving or interacting components, interface mounting patterns and tolerances, payload or cargo envelope, and installation access dimensions for maintenance.

---

### 4. Proactive Quality Checks

Continuously analyze the Design Values Library and its relationships to the requirements baseline, analysis models, and interface documents to surface the following issues:

#### 4.1 Orphaned Value Detection
- Flag any Active or Provisional value record with no entries in Referencing Requirement IDs, Referencing Analysis Model IDs, or Referencing Interface Document IDs.
- An orphaned value may indicate: a value created in anticipation of a requirement that was never written, a value that has been superseded but not retired, or a traceability gap where a model or requirement references the value informally rather than by Value ID.
- Generate an orphaned value report listing all orphaned records with owner, maturity stage, and date last modified.

#### 4.2 Undeclared Value Detection
- Flag any requirement statement that contains a numeric value with a unit that does not correspond to a registered Value ID in the library.
- A numeric value in a requirement that is not traceable to the library is an undeclared design value — it exists in the requirements baseline without governance, ownership, or change control.
- Generate an undeclared value report listing the requirement ID, the unregistered value, and the recommended library category for registration.

#### 4.3 Change Impact Analysis
- When any value record field is modified (value, unit, tolerance, or any tier), automatically identify and flag: all requirements referencing the Value ID, all analysis models referencing the Value ID, and all interface documents referencing the Value ID.
- Generate a change impact report listing all affected records, their current baseline status, and their verification status — previously closed verification activities linked to affected requirements must be flagged for re-verification review.
- Where a value change affects a Certified/Qualified Limit tier, escalate immediately to the library owner and the program certification or qualification lead.

#### 4.4 Maturity Violation Detection
- Flag any value record where the current Maturity Stage is below the defined Maturity Target for the current program phase.
- Flag any value with Source Type = Assumption at the second design review milestone or later — Assumed values are not permitted in Released Baseline requirements at that phase or beyond.
- Flag any Tiered Value where the Certified/Qualified Limit tier is still TBD at the pre-test readiness review milestone.
- Generate a maturity gap report organized by program phase, category, and owner.

#### 4.5 Conflict Detection
- Within each category, identify pairs of value records that define the same parameter with different values and no documented relationship (supersession, derivation, or intentional separation by scope).
- Flag values within CAT-PWR where a supply voltage range in one record is inconsistent with a consuming equipment voltage tolerance in another.
- Flag values within CAT-STRUCT where a load value in one record exceeds the structural limit in another without a documented margin.
- Flag values within CAT-SW where the sum of latency allocations across a signal chain exceeds the end-to-end latency limit for that chain.
- Generate a conflict report listing each conflict pair, the conflicting fields, and the owning engineers on each side for resolution.

---

### 5. Design Values Library Governance Principles

1. **One value, one record.** Every distinct numerical parameter has exactly one authoritative record in the library. If two records define the same parameter for different scopes, their scope distinction must be explicitly documented and their relationship defined.

2. **Requirements reference Value IDs, not raw numbers.** A requirement that states a numeric value must cite the governing Value ID in its traceability fields. A requirement with an embedded numeric value and no Value ID reference is an undeclared design value.

3. **Maturity must advance before a value can govern a Released Baseline requirement.** A value at Maturity Stage 1 (Assumed) may be referenced in a Draft or Preliminary Baseline requirement. It must reach at least Stage 2 (Analyzed) before the governing requirement may be set to Released Baseline.

4. **Value changes trigger requirement reviews.** Any change to a value record must generate an impact assessment covering all referencing requirements, models, and interface documents. The change is not complete until all affected records have been reviewed and their status updated.

5. **Superseded values are never deleted.** A superseded record is retained in the library with Status Tag = Superseded and a reference to the replacement record. The audit trail must be preserved for the life of the program.

6. **Physical constants are never program-specific.** CAT-PHY values are sourced exclusively from international or domain-authoritative standards. A physical constant with Source Type = Assumption or Analysis is a library error and must be corrected.

7. **The library is domain-configurable but structurally invariant.** Category names, maturity milestone labels, and default value sets may be adapted to the program's technical domain. The record schema, entry types, maturity model, status tags, and governance rules in this skill are invariant and apply to all programs equally.

---

## Dependencies & Interfaces

- **Depends on:** SK-REQ-001 — requirement writing rules governing numeric value expression.
- **Depends on:** SK-REQ-003 — requirements traceability baseline where value references are managed.
- **Extended by:** SK-VER-001 — verification data model consumes design values for pass/fail threshold governance.

---

## Changelog

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | [Date] | [Author] | Initial release. |
| 1.1 | [Date] | [Author] | Updated metadata and dependency interfaces to reflect SK-VER-001 consumption (`Extended By: SK-VER-001`). |
| 1.2 | [Date] | [Author] | Added explicit alignment to SE tool `designValue` entity fields (`name`, `description`, `value`, `unit`, `sourceReference`, `maturityStage`) and normalized maturity mapping to tool enums. |
