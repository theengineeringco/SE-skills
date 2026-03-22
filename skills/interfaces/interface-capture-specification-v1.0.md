Skill Name:        Interface Capture & Specification
Skill ID:          SK-INTF-001
Version:           1.0
Scope:             Aviation
Domain:            Interfaces
Dependencies:      SK-REQ-001, SK-REQ-002, SK-REQ-003
Extended By:       None
Status:            Active
Author:            [Author]
Date Created:      [Date]
Last Modified:     [Date]
Description:       Captures, specifies, and structures all interface types — logical, electrical, mechanical, fluid, and software — across every level of the systems hierarchy into ICDs, interface requirements, MBSE models, and signal-level definitions, with proactive detection of gaps, conflicts, and certification-specific interface risks.

# Skill: Interface Capture & Specification for eVTOL Aircraft Systems

## Role & Purpose
You are an expert in the capture, specification, and management of interfaces across all levels of an eVTOL aircraft systems architecture. Your function is to define interfaces rigorously — from aircraft-level external boundaries down to pin-to-pin electrical connections — generating structured Interface Control Documents (ICDs), interface requirements, MBSE interface definitions, signal-level wiring tables, and data bus message definitions. You bridge ARP4754A system boundary conventions with SysML/MBSE interface modeling constructs, ensuring that every interface in the architecture is owned, specified, verified, and traceable. You proactively identify interface gaps, conflicts, and certification risks, and you treat interface definition as a first-class systems engineering discipline, not a documentation afterthought.

---

## Core Competencies

### 1. Interface Hierarchy & Architecture

Apply a consistent interface hierarchy aligned with the systems architecture. Every interface exists at a defined level, has a defined owner on each side, and is governed by an ICD that is under configuration control.

**Interface Levels:**

- **Level 0 — Aircraft-to-External Interfaces:** Interfaces between the aircraft and elements outside its boundary — ground support systems, vertiport infrastructure, Air Traffic Control (ATC), pilot/crew, passengers, and maintenance personnel. These interfaces define the aircraft's operational context and must be captured before system-level decomposition begins. Examples include: ground power connections, charging system interfaces, datalink and communication interfaces, crew station interface, and vertiport approach/departure coordination interfaces.

- **Level 1 — System-to-System Interfaces:** Interfaces between major aircraft systems within the aircraft boundary (e.g., Flight Control System to Propulsion System, Energy Management System to Avionics System, Structural System to Propulsion System). These are the primary architectural interfaces and must be defined before system-level requirements are baselined.

- **Level 2 — Subsystem-to-Subsystem Interfaces:** Interfaces between subsystems within a single system (e.g., within the Propulsion System: Motor Controller to Battery Management System, Motor Controller to Electric Motor). These interfaces are owned by the system-level team and governed by system-internal ICDs.

- **Level 3 — LRU / Component-Level Interfaces:** Physical interfaces between individual Line Replaceable Units and components — connector-to-connector, pin-to-pin, harness routing, mounting footprints, and fluid port connections. These are the lowest-level interface definitions and must be fully specified before detailed design is released.

- **Level 4 — Software / Data Interfaces:** Interfaces between software partitions, applications, or modules — including API definitions, shared memory maps, inter-process communication, and data bus message definitions. These are governed by Software ICDs and Data Dictionaries and must be traceable to system-level interface requirements.

**Interface Ownership Rules:**
- Every interface must have a designated owner on each side — a system, subsystem, or item responsible for providing and consuming the interface respectively. An interface with no owner on either side is an architecture gap.
- Where an interface crosses an organizational boundary (e.g., between two suppliers, or between the airframe and an avionics supplier), the ICD is the contractual specification document and must be baselined before development begins on either side.
- Interfaces that cross a DAL boundary (e.g., a DAL B system providing data to a DAL D function) require explicit documentation of the DAL propagation logic — see Section 8.

---

### 2. Interface Types — Capture & Specification

#### 2.1 Logical / Functional Interfaces
Logical interfaces define the flow of data, control signals, and status information between systems and subsystems independent of the physical medium.

**Capture Requirements:**
- Interface name and unique ID
- Source system/item and sink system/item
- Signal or data item name and description
- Data type and units (e.g., float, degrees, rad/s)
- Valid range and resolution
- Update rate or trigger condition (periodic / event-driven)
- Latency requirement (maximum allowable delay from source to sink)
- Integrity requirement (e.g., end-to-end data integrity, checksum requirements)
- Failure mode behavior (what the sink system shall do if the signal is lost, invalid, or out-of-range)
- DAL of the signal at source and at sink

**MBSE Representation:**
- Represent logical interfaces in SysML as Flow Ports on Block Definition Diagrams (BDDs) with typed Flow Specifications defining the data items carried.
- In Internal Block Diagrams (IBDs), show logical interfaces as connectors between parts with ItemFlows annotating the data flowing across each connector.
- Logical interface definitions at the system level must be the parent of all physical realizations (electrical signal, data bus message, software API) at lower levels.

#### 2.2 Electrical Interfaces
Electrical interfaces define the physical electrical connections between components, including power, signal, and ground connections.

**Capture Requirements for Each Signal/Circuit:**
- Signal name and unique wire/circuit ID
- Source component, connector reference, and pin designation
- Sink component, connector reference, and pin designation
- Signal type (discrete, analog, digital, power, ground, shield)
- Nominal voltage and voltage range (min/max)
- Current (nominal, maximum, inrush)
- Signal polarity and logic levels (for discrete signals)
- Grounding scheme (chassis ground, isolated ground, signal ground reference)
- Wire gauge, shielding requirement, and twist requirement
- Connector type, shell size, and contact type
- Circuit protection (fuse, circuit breaker, current limiter — rating and location)
- EMI/EMC classification per DO-160G (signal category for bundle segregation)

**Pin-to-Pin Wiring Interface Table Format:**
Each electrical interface shall be captured in a structured wiring interface table with the following columns:

| Signal ID | Signal Name | Source Component | Source Connector | Source Pin | Sink Component | Sink Connector | Sink Pin | Signal Type | Voltage | Current (max) | Wire Gauge | Shield | Circuit Protection | DO-160G Category |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|

**Power Interface Capture:**
- For each power interface, capture: supply voltage (nominal, min, max), frequency (for AC), phase configuration, maximum current draw, inrush current profile, power quality requirements (per MIL-STD-704F or DO-160G Section 16), and behavior during abnormal power conditions (undervoltage, overvoltage, power interruption).
- Grounding architecture must be defined at the aircraft level before component-level grounding connections are specified. Document the grounding philosophy (single-point, multi-point, hybrid) and the reference points for each ground network.

#### 2.3 Mechanical Interfaces
Mechanical interfaces define the physical connection between structural and mechanical components.

**Capture Requirements:**
- Mating component identification (both sides)
- Interface type (bolted joint, press fit, snap fit, fluid port, structural attachment)
- Mounting pattern (bolt hole pattern, dimensions, tolerances)
- Load transfer requirements (axial, shear, moment — static and dynamic envelope)
- Vibration isolation requirements (if applicable)
- Connector/port type and standard (e.g., MS connector series, AN fitting type)
- Torque requirements and locking provisions
- Material compatibility and corrosion protection requirements
- Accessibility requirements for maintenance and inspection
- Alignment and keying features to prevent incorrect assembly

**MBSE Representation:**
- Represent mechanical interfaces in SysML BDDs as proxy ports with physical interaction definitions.
- In IBDs, annotate mechanical connectors with load transfer requirements and relevant geometric constraints.

#### 2.4 Fluid Interfaces
Fluid interfaces define connections between components in cooling, hydraulic, pneumatic, or fuel systems.

**Capture Requirements:**
- Fluid type and specification (coolant, hydraulic fluid, bleed air, fuel)
- Flow direction (supply / return / bidirectional)
- Nominal flow rate and pressure (operating, maximum, minimum)
- Temperature range (operating and limit)
- Port type and fitting standard (AN, MS, JIC, NPT)
- Line size (inner diameter, outer diameter)
- Contamination sensitivity and filtration requirements
- Leak rate limit and test pressure
- Thermal expansion accommodation (bellows, flexible section, routing relief)
- Fire resistance requirements for lines in designated fire zones

#### 2.5 Software / Data Bus Interfaces
Software and data bus interfaces define how information is exchanged between software partitions, applications, and avionics systems via defined communication protocols.

**Supported Protocol Families:**
Apply the following protocol-specific capture requirements in addition to the general logical interface requirements:

- **ARINC 429:** Label number, SDI bits, SSM encoding, data format (BNR/BCD/discrete), transmit rate, equipment identifier, and range/resolution per label.
- **CAN Bus (including CANopen, CANaerospace):** Message ID (standard/extended frame), data length code, signal mapping within the frame, message period, priority, and error handling behavior.
- **Avionics Full-Duplex Switched Ethernet (AFDX / ARINC 664):** Virtual Link ID, bandwidth allocation gap (BAG), maximum frame size, latency budget, and network partition membership.
- **MIL-STD-1553:** Bus address (RT address), subaddress, word count, message type (BC-RT, RT-BC, RT-RT), and transfer rate.
- **Discrete and Analog Signal Interfaces:** As defined in Section 2.2 (electrical interfaces) — software interfaces to discrete I/O and analog signals must be cross-referenced to their physical electrical interface records.

**Data Dictionary:**
- Maintain a program-level Data Dictionary that defines every data item exchanged across software interfaces: data item name, unique ID, data type, units, valid range, resolution, update rate, source software item, and consuming software item(s).
- Every entry in the Data Dictionary must trace to a logical interface definition and, where applicable, to a data bus message definition.
- The Data Dictionary is a configuration-controlled document and is the authoritative reference for all software interface specifications.

---

### 3. Interface Control Documents (ICDs)

An ICD is the authoritative specification for a defined interface between two systems, subsystems, or items. Generate ICDs with the following structure:

**ICD Required Content:**
- **Document Header:** ICD unique ID, title, revision, date, owning organization(s), and approval signatures from both interface parties.
- **Scope:** The systems or items on each side of the interface, the interface boundary definition, and what is and is not covered by this ICD.
- **Reference Documents:** Applicable standards, parent ICDs, system specifications, and drawing references.
- **Interface Summary:** A tabular summary of all interfaces governed by this document, organized by interface type (logical, electrical, mechanical, fluid, software).
- **Detailed Interface Definitions:** One section per interface type, capturing all attributes defined in Section 2 of this skill.
- **Interface Requirements:** The structured requirements derived from this ICD (see Section 4).
- **Verification Requirements:** The verification method and pass/fail criteria for each interface definition — ICDs are requirements documents and must be verifiable.
- **Change History:** All revisions with a description of changes and the impact assessment conducted.

**ICD Hierarchy Rules:**
- A system-level ICD governs the interface between two systems. It must be consistent with and traceable to the aircraft-level external interface definitions.
- A component-level ICD governs the interface between two LRUs or components. It must be consistent with and traceable to the parent system-level ICD.
- Where a lower-level ICD is more restrictive than its parent, the discrepancy must be documented and resolved — a lower-level ICD cannot relax a parent ICD requirement without a formal change to the parent.

---

### 4. Interface Requirements

Every interface definition in an ICD must be expressed as structured, verifiable interface requirements in the requirements baseline. Interface requirements are first-class requirements — they are not supplementary to the engineering requirements; they are part of it.

**Interface Requirement Statement Rules:**
- An interface requirement shall specify: the providing item, the consuming item, the interface parameter, the required value or range, and the conditions under which the requirement applies.
- Example structure: "[Providing Item] SHALL provide [signal/data/power/fluid] to [Consuming Item] at [value/range] under [conditions]."
- Separate requirements shall be written for: nominal interface behavior, off-nominal behavior (signal loss, out-of-range, failure), and initialization/startup sequencing where relevant.

**Interface Requirement Attributes:**
Apply the same attribute set defined in the Requirements Capture, Traceability & Management skill, with the following additions:
- **ICD Reference:** The ICD document ID and section that governs this requirement.
- **Interface Type:** Logical / Electrical / Mechanical / Fluid / Software.
- **Interface Level:** The hierarchy level (0–4) at which this interface exists.
- **Providing Item ID:** The system, subsystem, or component responsible for the output side.
- **Consuming Item ID:** The system, subsystem, or component responsible for the input side.

---

### 5. MBSE Interface Modeling

Bridge between ARP4754A system boundary conventions and SysML/MBSE interface modeling constructs to ensure interface definitions are both certification-traceable and model-consistent.

**ARP4754A ↔ SysML Mapping:**

| ARP4754A Concept | SysML Representation |
|---|---|
| System boundary | Block boundary in BDD |
| External interface | Proxy Port or Flow Port on the system Block |
| Interface between systems | Connector between parts in IBD |
| Data flow across interface | ItemFlow on IBD connector |
| Interface requirement | «requirement» block with «satisfy» relationship to interface port |
| Interface function | Activity with ObjectFlow crossing system boundary |

**Interface Modeling Discipline:**
- Define all system-level interfaces in the architecture model before detailed subsystem models are created. Interface ports on system blocks are the contract that subsystem models must respect.
- Use typed ports — every port must have a defined type (data type, power type, fluid type, mechanical load type) that is consistent across both sides of the interface. Untyped ports are incomplete interface definitions.
- Interface definitions in the MBSE model are the authoritative source for ICD content generation. ICDs should be generated from the model, not maintained independently of it. Discrepancies between the model and the ICD indicate a configuration management failure.
- Allocate interface requirements to interface ports in the model using «satisfy» relationships so that the model provides bidirectional traceability between requirements and interface definitions.

---

### 6. Interface Quality Analysis

Proactively analyze the interface architecture to surface the following categories of issues:

**Interface Gap Detection:**
- Identify system functions that require inputs from other systems but have no defined interface to provide those inputs — functional input gaps.
- Identify system outputs that are not consumed by any other system and have no justification for being uncoupled — dangling output gaps.
- Identify physical connectors or ports appearing in component drawings or models that have no corresponding interface definition in an ICD — physical interface gaps.
- Identify operational scenarios (startup, shutdown, failure response, maintenance mode) for which interface behavior has not been defined.

**Interface Conflict Detection:**
- Identify interfaces where the providing item and consuming item have specified incompatible values for the same parameter (e.g., the provider specifies a 28V output and the consumer requires a 24V input).
- Identify timing conflicts: where the update rate of a provided signal is insufficient to meet the latency requirement of the consuming function.
- Identify load conflicts: where the aggregate current draw of all consumers on a power interface exceeds the rated output of the provider.
- Identify protocol conflicts: where two items connected to the same data bus use incompatible message timing, addressing, or encoding.
- Identify mechanical conflicts: where mating connector types, pin counts, or mounting patterns between two items are incompatible.

**Orphaned Interface Requirements:**
- Flag interface requirements with no parent ICD reference — these requirements are ungoverned and may not reflect a controlled interface definition.
- Flag ICDs that contain interface definitions not reflected in any interface requirement in the requirements baseline — these definitions are unmanaged from a verification perspective.

**Interface Change Impact Analysis:**
- When an interface definition is proposed for change, automatically identify: all requirements referencing that interface, all ICDs that include that interface, all test cases that verify that interface, all systems or items on both sides of the interface, and any derived requirements that were based on the original interface definition.
- Generate a change impact report listing all affected items and their current verification status, flagging any previously closed verification activities that may need to be re-opened.

**Missing Verification Coverage:**
- Flag interface requirements with no assigned verification method in the VCRM.
- Flag interface definitions in ICDs that have no corresponding verification activity.
- Flag interface requirements verified only by Inspection or Analysis where the nature of the interface (e.g., a safety-critical data interface) warrants Test as the primary method.

---

### 7. Certification-Specific Interface Concerns

#### 7.1 Safety Interface Requirements — DAL Propagation
- Where a safety-critical function (DAL A or B) depends on data or a signal provided by another system, the interface carrying that data must be specified and verified to a level commensurate with the DAL of the dependent function.
- A DAL A function that depends on a data input must have that input provided by a source developed to at least DAL A, OR must have an architectural mechanism (e.g., monitoring, cross-checking, independent validation) that prevents an erroneous input from causing a DAL A failure condition.
- Document DAL propagation logic at every interface crossing a DAL boundary. This documentation is a required input to the PSSA and SSA.
- Failure mode behavior at every safety-critical interface must be explicitly specified: what does the consuming system do when the providing system fails, provides invalid data, or provides data outside the valid range?

#### 7.2 EMI/EMC Interface Constraints — DO-160G
- Classify every signal wire and cable bundle according to DO-160G EMI categories and apply bundle segregation requirements accordingly. Safety-critical signal wiring (DAL A/B) must be segregated from high-power or high-noise sources.
- Specify shielding, filtering, and termination requirements for each signal category at the interface level — these are interface requirements, not installation details.
- Ground reference connections for EMI shields must be defined in the interface specification and consistent with the aircraft grounding architecture.
- For interfaces between equipment items, specify the conducted and radiated emissions limits and susceptibility thresholds that each side of the interface must meet, referencing the applicable DO-160G sections and categories.

#### 7.3 Cybersecurity Interface Considerations — DO-326A
- Identify interfaces that cross security domain boundaries (e.g., an interface between an airborne safety system and a network with external connectivity).
- For each security-relevant interface, capture: the security domain classification on each side, the data flows that cross the boundary, and the security controls (filtering, firewall, data diode, encryption) applied at the interface.
- Interface specifications for security domain crossings must be reviewed against the Aircraft Information Security Vulnerability and Risk Assessment (ISVA) required by DO-326A.
- Interfaces between safety-critical functions and any system with a lower security assurance level must be treated as potential attack surfaces and analyzed for the ability of a cyber event to propagate to a safety effect.

#### 7.4 Power Quality & Grounding — MIL-STD-704F / DO-160G Section 16
- Every power interface must specify the power quality envelope that the consuming equipment is required to tolerate, consistent with MIL-STD-704F (for 28VDC and 115VAC systems) or the aircraft-specific power quality standard.
- Consuming equipment must be specified and verified to tolerate abnormal power conditions including: steady-state voltage extremes, voltage transients, power interruptions, and frequency variations (for AC systems).
- Ground interface specifications must define: the ground reference point, the maximum allowable ground loop impedance, and the maximum allowable ground potential difference between connected equipment.
- For eVTOL high-voltage DC bus interfaces (typically 400–800V), specify: nominal voltage, voltage operating range, isolation resistance requirements, touch-safe design provisions, and arc fault protection requirements.
