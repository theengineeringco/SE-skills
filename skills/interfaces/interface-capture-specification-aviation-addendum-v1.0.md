Skill Name:        Interface Capture & Specification — Aviation Addendum
Skill ID:          SK-INTF-001-AVN
Version:           1.0
Scope:             Aviation
Domain:            Interfaces
Dependencies:      SK-REQ-001, SK-REQ-002, SK-REQ-003, SK-REQ-003-AVN, SK-INTF-001, SK-CERT-001
Extended By:       None
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Extends the base Interface Capture & Specification skill for FAA aviation certification programs by adding DAL propagation rules at interface boundaries, EMI/EMC interface constraints, cybersecurity interface considerations, and power quality and grounding requirements.

---

# Skill: Interface Capture & Specification — Aviation Certification Addendum

## Purpose & Relationship to Base Skill

This addendum extends SK-INTF-001 for use in FAA aviation certification programs. All base skill rules — interface hierarchy, interface type capture requirements, ICD structure, MBSE modeling discipline, and quality analysis — remain fully in force. This addendum adds the following aviation-specific content:

- Section A: DAL Propagation at Interface Boundaries (extends base Section 1 ownership rules)
- Section B: Extended Wiring Interface Table (extends base Section 2.2 electrical capture)
- Section C: EMI/EMC Interface Constraints — DO-160G
- Section D: Cybersecurity Interface Considerations — DO-326A
- Section E: Power Quality & Grounding — MIL-STD-704F / DO-160G Section 16
- Section F: eVTOL-Specific Interface Concerns

Where this addendum conflicts with the base skill, this addendum takes precedence for aviation certification work.

---

## Section A: DAL Propagation at Interface Boundaries

This section replaces the general assurance level boundary note in SK-INTF-001 Section 1 for aviation certification programs. DAL is defined in SK-CERT-001.

**DAL Propagation Rules:**
- Where a safety-critical function (DAL A or B) depends on data or a signal provided by another system, the interface carrying that data must be specified and verified to a level commensurate with the DAL of the dependent function.
- A DAL A function that depends on a data input must have that input provided by a source developed to at least DAL A, OR must have an architectural mechanism (e.g., monitoring, cross-checking, independent validation) that prevents an erroneous input from causing a DAL A failure condition.
- Document DAL propagation logic at every interface crossing a DAL boundary. This documentation is a required input to the PSSA and SSA per ARP4754A.
- Failure mode behavior at every safety-critical interface must be explicitly specified: what does the consuming system do when the providing system fails, provides invalid data, or provides data outside the valid range?

**DAL Boundary Interface Attributes:**
Add the following fields to the base wiring interface table and logical interface capture for all interfaces crossing a DAL boundary:

| Field | Description |
|---|---|
| Source DAL | DAL of the providing system or item |
| Sink DAL | DAL of the consuming system or item |
| DAL Boundary Crossed | Yes / No |
| DAL Propagation Mechanism | Direct (source DAL ≥ sink DAL) / Monitored / Cross-checked / Independent validation |
| PSSA Reference | ID of the PSSA section documenting the DAL propagation argument |

**Independence Interface Requirements:**
- Where the PSSA requires independence between two functions, interfaces between those functions must be specified to prevent any shared resource, common failure mode, or cascading fault from bridging the independence boundary.
- Independence interface requirements must be written using SK-REQ-002 Pattern S3 and must identify both the independent functions and the interface pathway that must not bridge them.

---

## Section B: Extended Wiring Interface Table for Aviation

Replace the base skill wiring interface table format (SK-INTF-001 Section 2.2) with the following extended format for aviation programs, which adds DO-160G EMI category and DAL classification columns:

| Signal ID | Signal Name | Source Component | Source Connector | Source Pin | Sink Component | Sink Connector | Sink Pin | Signal Type | Voltage | Current (max) | Wire Gauge | Shield | Circuit Protection | DO-160G Category | Source DAL | Sink DAL |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|

**DO-160G Category Assignment Rules:**
- Classify every signal wire and cable bundle according to DO-160G EMI categories and apply bundle segregation requirements accordingly.
- Safety-critical signal wiring (DAL A/B) must be segregated from high-power or high-noise sources per DO-160G bundle segregation requirements.
- The DO-160G category assignment must be consistent with the equipment qualification category selected in the Equipment Qualification Test Plan governed by SK-VV-001.

---

## Section C: EMI/EMC Interface Constraints — DO-160G

**Bundle Segregation:**
- Classify every signal wire and cable bundle according to DO-160G EMI categories and apply bundle segregation requirements accordingly.
- Specify shielding, filtering, and termination requirements for each signal category at the interface level — these are interface requirements, not installation details.
- Ground reference connections for EMI shields must be defined in the interface specification and consistent with the aircraft grounding architecture.

**Equipment Interface EMC Requirements:**
- For interfaces between equipment items, specify the conducted and radiated emissions limits and susceptibility thresholds that each side of the interface must meet, referencing the applicable DO-160G sections and categories.
- EMC interface requirements must be verified by test per DO-160G at the equipment qualification level — Analysis alone is not acceptable for DAL A/B equipment EMC compliance.

**Lightning Interface Requirements:**
- For interfaces between equipment items where lightning transient propagation is possible, specify the lightning transient withstand requirements per DO-160G Sections 22 and 23.
- Lightning protection requirements must be coordinated with the aircraft-level lightning zoning analysis.

---

## Section D: Cybersecurity Interface Considerations — DO-326A

**Security Domain Boundary Identification:**
- Identify all interfaces that cross security domain boundaries (e.g., an interface between an airborne safety system and a network with external connectivity).
- For each security-relevant interface, capture: the security domain classification on each side, the data flows that cross the boundary, and the security controls (filtering, firewall, data diode, encryption) applied at the interface.

**Security Interface Requirements:**
- Interface specifications for security domain crossings must be reviewed against the Aircraft Information Security Vulnerability and Risk Assessment (ISVA) required by DO-326A.
- Interfaces between safety-critical functions and any system with a lower security assurance level must be treated as potential attack surfaces and analyzed for the ability of a cyber event to propagate to a safety effect.
- Security interface requirements must identify: the threat categories mitigated, the security control mechanism, and the verification method for the security control.

**Security Interface Attributes:**
Add the following fields to interface records crossing a security domain boundary:

| Field | Description |
|---|---|
| Security Domain — Source | Security domain classification of the providing item |
| Security Domain — Sink | Security domain classification of the consuming item |
| Security Boundary Crossed | Yes / No |
| Security Control Mechanism | Filter / Firewall / Data Diode / Encryption / None |
| ISVA Reference | Reference to the ISVA threat analysis covering this interface |

---

## Section E: Power Quality & Grounding — MIL-STD-704F / DO-160G Section 16

**Power Quality Interface Requirements:**
- Every power interface must specify the power quality envelope that the consuming equipment is required to tolerate, consistent with MIL-STD-704F (for 28VDC and 115VAC systems) or the aircraft-specific power quality standard.
- Consuming equipment must be specified and verified to tolerate abnormal power conditions including: steady-state voltage extremes, voltage transients, power interruptions, and frequency variations (for AC systems).

**Grounding Interface Requirements:**
- Ground interface specifications must define: the ground reference point, the maximum allowable ground loop impedance, and the maximum allowable ground potential difference between connected equipment.
- The aircraft grounding architecture must be defined at the aircraft level before component-level grounding connections are specified. Document the grounding philosophy (single-point, multi-point, hybrid) and the reference points for each ground network.

**Power Interface Attributes — Aviation Extension:**
Add the following fields to power interface records for aviation programs:

| Field | Description |
|---|---|
| Power Quality Standard | MIL-STD-704F / DO-160G Section 16 / Program-specific |
| Voltage Transient Withstand | Maximum transient voltage the consuming equipment must tolerate (V, duration) |
| Power Interruption Tolerance | Maximum power interruption duration the consuming equipment must tolerate (ms) |
| Ground Reference Point | Designated ground reference for this interface |
| Ground Loop Impedance Limit | Maximum allowable ground loop impedance (Ω) |

---

## Section F: eVTOL-Specific Interface Concerns

**High-Voltage DC Bus Interfaces (400–800V):**
- For eVTOL high-voltage DC bus interfaces, specify: nominal voltage, voltage operating range, isolation resistance requirements, touch-safe design provisions, and arc fault protection requirements.
- High-voltage interface specifications must address: pre-charge circuit requirements, contactor sequencing, insulation monitoring, and ground fault detection.
- High-voltage wiring interface records must include additional fields: isolation class, creepage and clearance distances, and high-voltage warning labeling requirements.

**Vertiport & Ground Infrastructure Interfaces:**
- Capture interfaces between the aircraft and vertiport infrastructure as Level 0 interfaces per SK-INTF-001 Section 1, including: ground power connections, charging system interfaces, data connectivity, and aircraft health monitoring data feeds.
- Vertiport interface specifications must be consistent with ASTM F3548 (Vertiport Design) requirements for the applicable interface parameters.
- Ground charging interface requirements must specify: charging protocol (e.g., CCS, CHAdeMO, proprietary), maximum charge current, communication handshake requirements, and safety interlock conditions.

**Electric Propulsion System Interfaces:**
- Motor controller to battery management system interfaces must specify: high-voltage bus voltage range, current demand signaling, state of charge feedback, thermal status signals, and fault/inhibit discrete signals.
- Motor controller to electric motor interfaces must specify: phase voltage and current, PWM frequency, thermal sensor signals, resolver or encoder feedback, and mechanical brake control signals.

---

## Anti-Patterns — Aviation Additions

Add the following to the base skill anti-pattern table:

| Anti-Pattern | Violation | Action |
|---|---|---|
| DAL A/B interface with no failure mode behavior specified | Safety-critical interface without failure response — certification risk | Add off-nominal interface requirement using SK-REQ-002 Pattern I2 |
| Interface crossing DAL boundary with no propagation argument | Unsubstantiated safety claim | Document DAL propagation mechanism and PSSA reference per Section A |
| EMC category not assigned to safety-critical signal wiring | DO-160G segregation requirement unaddressed | Assign DO-160G category and update wiring table per Section B |
| Security domain crossing with no security control specified | Potential cyber-to-safety propagation path unmitigated | Add security control and ISVA reference per Section D |
| HV DC interface without isolation resistance requirement | Safety gap for touch-hazard protection | Add isolation resistance and touch-safe design requirements per Section F |
| Vertiport charging interface not captured as Level 0 ICD | External interface gap | Create Level 0 ICD per SK-INTF-001 Section 1 and ASTM F3548 |

---

## Dependencies & Interfaces

- **Extends:** SK-INTF-001 — all base rules remain in force
- **Depends on:** SK-REQ-001 (interface requirement writing), SK-REQ-002 (aviation interface requirement patterns), SK-REQ-003 (requirements traceability), SK-REQ-003-AVN (DAL allocation at interface boundaries), SK-CERT-001 (DAL definition, DO-160G, DO-326A, MIL-STD-704F authority)
- **Provides to:** SK-INTF-002 — aviation-specific interface classification for change control tier assignment
- **Provides to:** SK-VV-001 — DO-160G category assignments as input to environmental qualification planning

---

## Changelog

| Version | Date | Author | Summary of Changes |
|---|---|---|---|
| 1.0 | [Date] | [Author] | Initial release — content migrated from SK-INTF-001 v1.0 (aviation scope) and extended with DAL propagation attributes, DO-160G extended wiring table, cybersecurity interface attributes, power quality attributes, and eVTOL-specific HV and vertiport interface content. |

---

*Authority: SAE ARP4754A (2010) | RTCA DO-160G | RTCA DO-326A (2014) | MIL-STD-704F | ASTM F3548 | Extends: SK-INTF-001 v2.0*
