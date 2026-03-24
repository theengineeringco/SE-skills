Skill Name:        Requirements Writing — Aviation Certification Addendum
Skill ID:          SK-REQ-002
Version:           1.0
Scope:             Aviation
Domain:            Requirements
Dependencies:      SK-REQ-001
Extended By:       None
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Extends the base Requirements Writing skill for FAA certification programs by adding aviation-specific requirement types, DAL-aware authoring rules, safety and interface requirement patterns, derived requirement discipline, Similarity as a fifth verification method, and aerospace anti-patterns aligned with ARP4754A, ARP4761, and AC 25.1309.

# Requirements Writing Skill — Aviation Certification Addendum
**Extends:** Requirements Writing Skill v2.0 (INCOSE GtWR v4 / EARS)
**Authority:** ARP4754A, ARP4761, DO-178C, DO-254, FAA AC 25.1309, AC 23.1309
**Scope:** eVTOL aircraft requirements written for FAA certification programs
**Version:** 1.0

---

## PURPOSE & RELATIONSHIP TO BASE SKILL

This addendum extends the base Requirements Writing Skill for use in aviation certification programs. All base skill rules (R1–R11), EARS patterns, quality characteristics (Q1–Q9), and anti-patterns remain in full force. This addendum adds aviation-specific requirement types, writing patterns, DAL-aware authoring rules, expanded verification methods, and aerospace anti-patterns that the base skill does not address. Where this addendum conflicts with the base skill, this addendum takes precedence for aviation certification work.

Scope boundary: This addendum covers requirements written for FAA-certificated aircraft programs. It does not replace SK-REQ-001 — all base rules remain in force. For requirements capture, traceability, and management see SK-REQ-003. For verification method assignment at the program level see SK-VV-001.
Data model alignment: when used with the SE tool data model skill, store method assignment in `verificationMethod` (enumArray: `Test|Analysis|Inspection|Demonstration|Similarity`) and status in `verificationStatus` (enum: `Passed|Failed|Pending|Not Applicable|In Progress`) on the `requirement` entity.
DAL: Development Assurance Level assigned per ARP4754A. Authoritative definition in SK-CERT-001. This skill applies DAL to requirement writing and verification method selection.
Verification methods recognized by this skill: Test, Inspection, Analysis, Demonstration, Similarity (per ARP4754A Table 7 and SK-REQ-001 base definitions).

---

## SECTION A: REQUIREMENT TYPE CLASSIFICATION

Before writing or reviewing any requirement in an aviation certification program, classify it by type. Type classification drives pattern selection, DAL implications, and verification method assignment. Every requirement output shall include a TYPE field.

| Type ID | Type Name | Definition | Primary EARS Pattern |
|---|---|---|---|
| FUNC | Functional | Defines a capability or behavior the system shall perform | Ubiquitous, State-Driven, Event-Driven |
| PERF | Performance | Defines a measurable bound on how well a function is performed | Ubiquitous (with numeric criterion) |
| SAFE | Safety | Derived from FHA/PSSA; defines a failure condition constraint, probability target, or independence obligation | Conditional, Event-Driven, Ubiquitous |
| INTF | Interface | Defines the obligation of a providing or consuming item at a system boundary | Ubiquitous, State-Driven, Conditional |
| DERV | Derived | Introduced by a design decision with no direct parent stakeholder need; not decomposed from a higher-level requirement | Any |
| OPER | Operational | Defines constraints on how the system is operated, maintained, or supported | State-Driven, Conditional |
| CONF | Conformance | Captures a regulatory or standards compliance obligation | Ubiquitous, Conditional |

**Classification Rules:**
- A requirement may carry only one primary type. If a requirement appears to span two types, it likely contains two obligations — apply Rule R1 (Singular) and split it.
- SAFE requirements must always be traceable to a named failure condition in the FHA or PSSA. A safety requirement with no FHA/PSSA parent is an orphaned safety requirement and must be flagged.
- DERV requirements must include a RATIONALE field in all output formats explaining the design decision that introduced them and confirming that a safety assessment has been notified.
- CONF requirements shall cite the specific regulatory reference (e.g., 14 CFR § 25.1309, ARP4754A Section 5.3) as part of the requirement statement or in the rationale.

---

## SECTION B: DAL-AWARE REQUIREMENT WRITING

The Development Assurance Level (DAL) assigned to a requirement under ARP4754A affects how the requirement must be written, what verification rigor is required, and what independence obligations must be stated. Apply the following rules when DAL is known or can be inferred.

**DAL Assignment in Requirement Attributes:**
Every requirement in an aviation certification program shall carry a DAL attribute (A, B, C, D, or E) in its output record. If DAL has not yet been assigned at the time of writing, the field is marked TBD and flagged for resolution before the requirements baseline is finalized.

**DAL-Driven Writing Rules:**

| DAL | Writing Obligation |
|---|---|
| A | Performance criteria must be fully quantified — no TBD values, no ranges without explicit bounds. Failure behavior must be explicitly stated. Independence requirements must be written as explicit requirements, not left to the architecture. |
| B | Performance criteria must be quantified. Failure behavior should be stated where the function is safety-relevant. Independence requirements must be written where ARP4754A requires them. |
| C | Performance criteria should be quantified. Failure behavior stated where relevant to system-level safety objectives. |
| D/E | Standard base skill rules apply. No additional DAL-specific obligations. |

**DAL A/B Failure Behavior Rule:**
For every DAL A or B functional or performance requirement, write a companion failure behavior requirement that explicitly states what the system shall do when the function fails, the input is lost, or the output is out of range. A DAL A functional requirement with no failure behavior companion is an incomplete requirement set.

Example companion pair:
```
FUNC/DAL A:
The flight control system shall maintain the commanded roll attitude within ±2 degrees
under all flight conditions within the normal flight envelope.

SAFE/DAL A (companion):
When the primary roll attitude sensor output is invalid or absent, the flight control
system shall revert to the secondary roll attitude source within 50 milliseconds and
annunciate the sensor failure to the crew.
```

---

## SECTION C: REQUIREMENT TYPE PATTERNS

### C.1 Safety Requirement Patterns

Safety requirements are derived from the FHA/PSSA and must express one of three safety obligation types: a failure condition constraint, a quantitative probability target, or a development/operational independence obligation.

**Pattern S1 — Failure Condition Constraint:**
States that a defined failure condition shall not occur, or constrains its effect.
```
Template:
The <subject> shall not exhibit <failure condition description> under <operating conditions>.

Example:
The propulsion management system shall not command simultaneous reduction of thrust on
more than one motor group during any single failure condition within the normal flight envelope.
```

**Pattern S2 — Quantitative Probability Target:**
States the maximum allowable probability of a failure condition per flight hour, derived from AC 25.1309 or the agreed certification basis.
```
Template:
The probability of <failure condition> occurring shall not exceed <value> per flight hour.

Example:
The probability of loss of all thrust occurring shall not exceed 1×10⁻⁹ per flight hour.
```
*Note: Probability target requirements are verified by Analysis (safety assessment) — never by Test alone.*

**Pattern S3 — Independence Obligation:**
States that two functions, items, or development processes shall be independent, with the independence claim traceable to the safety assessment.
```
Template:
The <Function/Item A> shall be designed and implemented independently of <Function/Item B>
such that no single failure, common cause event, or shared resource can affect both.

Example:
The primary flight control computation shall be designed and implemented independently
of the energy management computation such that no single failure, common cause event,
or shared software module can affect both functions simultaneously.
```

**Safety Requirement Writing Rules:**
- Every safety requirement shall reference its parent failure condition by FHA/PSSA identifier in the rationale or traceability field.
- Probability target requirements (Pattern S2) shall state the unit explicitly as "per flight hour" — never "per operation," "per mission," or unqualified.
- Independence obligation requirements (Pattern S3) shall identify both items and state the independence claim. "Shall be independent" without naming both parties is incomplete.
- Safety requirements shall never use escape clauses (R4). A safety requirement containing "where possible," "as appropriate," or "to the extent practicable" is a critical violation.

---

### C.2 Interface Requirement Patterns

Interface requirements define the obligation of a providing item, a consuming item, or both at a defined system boundary. They must identify both parties and the interface parameter explicitly.

**Pattern I1 — Provider Obligation:**
States what the providing item shall deliver at the interface.
```
Template:
The <providing item> shall provide <signal/data/power/fluid parameter> to the
<consuming item> at <value/range> under <operating conditions>.

Example:
The battery management system shall provide the remaining energy state to the energy
management computer as a value in the range 0–100 percent state of charge, with a
resolution of 0.1 percent and an update rate of not less than 10 Hz, under all
normal and abnormal operating conditions.
```

**Pattern I2 — Consumer Obligation:**
States what the consuming item shall do upon receiving or losing an interface input.
```
Template:
When <interface input condition>, the <consuming item> shall <response action>
[within <time bound>].

Example:
When the airspeed data bus input to the flight control computer is absent or flagged
invalid for more than 100 milliseconds, the flight control computer shall revert to
the reversionary airspeed source and annunciate the data loss to the crew.
```

**Pattern I3 — Bilateral Interface Constraint:**
States a constraint that both sides of the interface must satisfy simultaneously.
```
Template:
The interface between <Item A> and <Item B> shall conform to <standard/specification>
with respect to <parameter> under <conditions>.

Example:
The interface between the motor controller and the propulsion management computer shall
conform to ARINC 429 label encoding and timing requirements for all transmitted
parameters under all normal and abnormal power conditions.
```

**Interface Requirement Writing Rules:**
- Every interface requirement shall identify the providing item and consuming item by name — "the system" or "the interface" as subject is a violation of R3 (Specific Subject).
- Interface requirements for safety-critical signals (DAL A/B) must include a failure behavior companion requirement (Pattern I2) stating what the consumer shall do when the signal is lost or invalid.
- Interface requirements shall reference the governing ICD document ID in the rationale or traceability field.
- Units of measure (R6) are mandatory for every interface parameter — voltage, current, frequency, data rate, update rate, pressure, flow rate, and all other quantitative interface attributes must carry explicit units.

---

### C.3 Derived Requirement Pattern

Derived requirements are introduced by design decisions and have no direct parent stakeholder or regulatory need. They must be explicitly identified and their origin documented.

```
Template:
[Standard EARS pattern for the functional obligation, with DERV type tag and mandatory rationale]

Required RATIONALE content for all DERV requirements:
1. The design decision that introduced this requirement
2. The system or item that made the decision
3. Confirmation that the safety assessment team has been notified
4. The FHA/PSSA impact determination (New failure mode introduced: Yes/No)

Example:
The motor controller shall perform a built-in test of the inverter gate driver circuits
within 500 milliseconds of power application and shall inhibit motor torque output if
any gate driver fault is detected.

TYPE: DERV
RATIONALE: Introduced by the motor controller detailed design decision to use discrete
gate driver ICs rather than an integrated inverter module. Decision owner: Propulsion
Subsystem team. Safety assessment notified: Yes. New failure mode introduced: Yes —
nuisance inhibit on false BIT failure. PSSA updated to include this failure mode.
```

---

## SECTION D: VERIFICATION METHOD EXTENSIONS

The base skill defines four verification methods: Test, Inspection, Analysis, Demonstration. This addendum adds **Similarity** as a fifth method, consistent with ARP4754A Table 7, and adds aviation-specific assignment rules.

### D.1 Similarity — Definition & Use Conditions

| Method | Definition | Use Conditions |
|---|---|---|
| **Similarity** | Compliance is demonstrated by showing that a previously certified item or system is sufficiently similar to the current design that prior compliance evidence remains valid. | A previously certified item exists; all differences have been characterized; an engineering assessment confirms differences do not invalidate prior evidence; FAA concurrence obtained for DAL A/B. |

**Similarity Assignment Rules:**
- Similarity shall never be assigned as the sole verification method for a DAL A safety requirement without prior FAA ACO concurrence documented in the certification plan.
- Every requirement verified by Similarity must reference the Similarity Analysis Report (SAR) ID in the VCRM.
- Where differences between the similar item and the current design affect the requirement being closed, supplemental verification activities must be added and the verification method updated to Similarity + [supplemental method].

### D.2 ARP4754A-Aligned Verification Method Assignment Rules

Apply the following rules in addition to the base skill assignment guidance:

| Requirement Type | Preferred Method | Acceptable Alternatives | Not Acceptable |
|---|---|---|---|
| FUNC / DAL A or B | Test | Analysis (if validated model) | Inspection alone, Similarity alone |
| FUNC / DAL C or D | Test or Analysis | Inspection, Similarity | — |
| PERF / DAL A or B | Test | Analysis (with model validation evidence) | Inspection, Demonstration |
| PERF / DAL C or D | Test or Analysis | Demonstration | — |
| SAFE (probability target) | Analysis | — | Test alone, Inspection, Similarity alone |
| SAFE (independence obligation) | Analysis + Inspection | Test | — |
| INTF / DAL A or B | Test | Analysis | Inspection alone |
| INTF / DAL C or D | Test or Inspection | Analysis, Similarity | — |
| DERV | Per functional type above | — | — |
| CONF | Inspection or Analysis | — | — |

---

## SECTION E: AVIATION CERTIFICATION ANTI-PATTERNS

Add the following anti-patterns to the base skill anti-pattern table. Flag without exception.

| Anti-Pattern | Violation | Action |
|---|---|---|
| "…shall be safe…" *(unqualified)* | "Safe" is undefined without a failure condition reference | Replace with a specific safety requirement pattern (S1, S2, or S3) referencing the FHA failure condition |
| "…shall not fail…" | Absolute prohibition on failure is unverifiable and not certification-meaningful | Replace with a probability target (Pattern S2) and a failure behavior requirement |
| "…shall be independent…" *(without naming both items)* | Independence claim is incomplete | Rewrite using Pattern S3 naming both items and the shared resource or failure mode being excluded |
| "…per the ICD…" *(as the complete requirement)* | Delegation to a document is not a requirement | Write the specific interface obligation using Pattern I1, I2, or I3; reference the ICD in rationale |
| "…shall comply with ARP4754A…" *(as the complete requirement)* | Standards compliance is not a system requirement | Decompose into specific functional, process, or safety requirements; use CONF type with specific section reference |
| "…shall meet DAL [X]…" | DAL is a development assurance attribute, not a system requirement | Remove from requirement statement; assign DAL as a requirement attribute in the VCRM |
| Probability target without "per flight hour" unit | Ambiguous probability metric | Add "per flight hour" explicitly |
| Safety requirement with escape clause | Safety obligations cannot be qualified | Remove all escape clauses; safety requirements are unconditional |
| Derived requirement with no rationale | Unmanaged design decision in the requirements baseline | Add DERV rationale block per Section C.3 |
| Interface requirement with no named providing and consuming item | Interface is unowned | Rewrite using Pattern I1, I2, or I3 with both parties named |
| "…shall support compliance with…" | "Support" is ambiguous (base R7 applies); compliance obligations must be specific | Replace with specific CONF requirement citing the standard section |
| TBD/TBR values in DAL A or B requirements | Incomplete safety-critical obligation | Resolve TBD/TBR before baseline; flag as a critical gap if present at CDR |

---

## SECTION F: UPDATED OUTPUT FORMAT EXTENSIONS

Add the following fields to all three base skill output formats (Generate, Review, Improve) when operating in an aviation certification context:

```
TYPE: [FUNC | PERF | SAFE | INTF | DERV | OPER | CONF]
DAL: [A | B | C | D | E | TBD]
PARENT REQUIREMENT ID: [ID of parent requirement, or "Derived — see rationale" for DERV]
ICD REFERENCE: [Governing ICD document ID, if INTF type — otherwise "N/A"]
FHA/PSSA REFERENCE: [Governing failure condition ID, if SAFE type — otherwise "N/A"]
FAILURE BEHAVIOR COMPANION REQUIRED: [Yes | No] — Yes if DAL A or B FUNC or INTF requirement
```

---

*Authority: SAE ARP4754A (2010) | SAE ARP4761 (1996) | RTCA DO-178C (2011) | RTCA DO-254 (2000) | FAA AC 25.1309-1B | FAA AC 23.1309-1E | Extends: Requirements Writing Skill v2.0 (INCOSE GtWR v4 / EARS)*
