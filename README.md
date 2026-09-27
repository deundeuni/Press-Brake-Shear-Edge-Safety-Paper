# Press-Brake-Shear-Edge-Safety-Paper — Proximity Safety System and Local AI Edge Autonomous Survival Control Architecture for Press Brakes, Shears, Roll Benders, Notchers, and Sheet Metal Machinery (v1.53 Prior-Art Refined Baseline)

> Notice of Original Authority: The primary legal and engineering authority of this technical specification resides in the Korean original (README.ko.md). README.md serves as a secondary English reference. In case of any discrepancy, the Korean original shall prevail.

> Upper-Level Universal Architecture Association Notice: This whitepaper is organized as a stationary machine tool sub-whitepaper under Machine-Tools-Edge-Safety-Paper, the top-level master repository for universal machine tools, and operates in conjunction with the philosophy of the top-level hub soma-moa.

---

## Executive Summary

* Design Purpose & Survival Philosophy — Establishes a lightweight, ultra-low-latency survival control architecture that assists workers' practical safety while coexisting with existing equipment without forcing machine replacement. Creating a reassuring work environment rather than worker surveillance is set as the top priority.
* Core Mechanism Specifications — Integrates 5mm offset auxiliary fingers complying with EN 12622 and ISO 13857/13854, continuous Quiet Assist during manual micro-machining under 10mm or safeguard bypass/muting, decelerated descent/rotation below Mute Point (substantially attenuating kinetic energy by (10/200)^2 = 1/400 to prevent musculoskeletal occupational diseases), and eFPGA 0.1ms ultra-low-latency hardware cutoff with immediate origin ascent/reverse recovery logic.
* Power & Sensor Fusion System — Combines normally de-energized EPM/mechanical latch-based inertia/free-fall prevention during abrupt power outages with auto-restart blocking upon power restoration (soma-moa emergency power integration), IEC 60204-1 non-invasive contact interfacing, triple-sensor fusion (60GHz FMCW radar, thermal imaging, capacitive copper foil), and a background lightweight local AI analysis agent.
* Safety Governance & Licensing — Integrates Safety-II (assisting continuity of normal operation) and Just Culture (PII 10-second destruction) frameworks with a T-Reg 15% performance degradation mode, applying dual licensing: CC BY 4.0 for document copyrights and Apache License 2.0 (Apache-2.0) for derived code and executable implementations.

---

## 1. Designer's Declaration & Core Claims

### Architectural Conception
This architecture specification was established to prevent worker accidents frequently occurring across high-load pinching and shearing hazard sheet metal and forming machinery—including press brakes, shears, cutting machines, roll benders, pipe/tube benders, notchers, ironworkers (combination sheet metal machines), roll formers, coil cut-to-length/slitting lines, sheet levelers/straighteners, and crimping/riveting presses. Without relying on communication networks or upper-level servers, an autonomous survival control structure is established to immediately induce motor stop and reverse clearance via role separation between edge-localized hardware (eFPGA) ultra-low-latency triggering and background lightweight local AI analysis. The overall design authority for this architecture belongs to the designer (deundeuni).

### Software Utility Limitation
Tools utilized during the creation of this document are limited to passive execution utilities that performed formatting and contextual refinement based on the architectural logic and edge autonomous control scope defined by the designer.

### 10 Core Mechanisms & Prior-Art Fork Points
* 5mm Offset Auxiliary Finger Physical Structure — Incorporates a lightweight structure with built-in 1.5T spring elasticity (150/80mm spec) complying with ISO 13857 upper/lower limb reach prevention and ISO 13854 minimum gap standards, simultaneously performing support and pushing within 5mm of V-dies, shear blades, and roller inlets to physically mitigate access to pinch points.
* Mute Point-Coupled Decelerated Descent/Rotation, Ultra-Low Latency Cutoff, and Immediate Safety Height (Origin) Ascent / Reverse Recovery Logic — Interlocks with EN 12622 slow speed (10mm/s or lower Safe Speed) and Mute Point profile settings (analogously applied to derivative sheet metal machinery). Based on kinetic energy square-proportional relationship ($E_k \propto v^2$), the deceleration ratio ((10/200)^2 = 1/400) substantially attenuates inertial/hydraulic impact, suppresses bounce, mitigates worker startle reflexes, and prevents musculoskeletal occupational diseases. Upon detecting anomalies, eFPGA 0.1ms hardware cutoff control induces immediate ascent to safety height (origin) or roller reverse recovery.
* Quiet Assist Continuous Maintenance Logic During Under-10mm Manual Micro-Machining and Safeguard Bypass/Mute — During small component trimming, corner notching, remnant processing, or physical bypass of existing optical sensors, independent triple sensors and eFPGA hardware interlocks remain active without nuisance tripping, performing continuous monitoring and ultra-low-latency cutoff as a "silent final auxiliary."
* Abrupt Power Outage Response: Normally De-Energized EPM / Mechanical Latch and Power-Restoration Auto-Restart Blocking Logic — Upon sudden power failure, upper ram free-fall and roller inertial rotation due to hydraulic/power loss are physically attenuated and locked within 0.1ms using normally de-energized electro-permanent magnets (EPM) or mechanical latches (spring-based fail-safe brakes or pneumatic brakes). Upon power restoration, the RECOVERY latch state is maintained to prevent unauthorized auto-restart and unexpected strokes, integrated with soma-moa emergency power survival framework.
* 5mm Proximity Bending/Forming/Rolling Exception-Handling Safety Assist — Avoids indiscriminate cutoff within 5mm of V-dies, roller pinch points, or punches; when triple sensors determine a safe posture, processing continues uninterrupted, while immediate cutoff and origin ascent/reverse recovery are triggered if posture deviates into a hazard area.
* Alarm Fatigue Mitigation & Tooling/Roller Geometry-Coupled Risk Rating Logic — Based on ANSI B11.3, ANSI B11.12, and ISO 12100 risk assessments, dynamically adjusts risk weightings by recognizing upper/lower die profiles, roller curvature, wiper die clearance, and stroke ranges. Suppresses nuisance trips when worker body positions remain in safe clearance outside physical crush lines, encouraging safeguards to remain active.
* Dual-Operating Mode Governance (Normal Safety Mode vs. Special-Purpose Tooling Mode) — Classifies control layers into strict physical protection mode for standard operations and dual-operating mode for special-purpose geometries (large roll bending, gooseneck dies, notching, micro-cutting) authenticated via UWB/physical keys, securing operational efficiency and protection reliability simultaneously.
* soma-moa Modernized Safety Framework Integration (Safety-II & Just Culture) — Reinterprets Heinrich's 1931 philosophy into modern resilience engineering by focusing on supporting the continuity of overwhelming normal operations (Safety-II) and Just Culture (PII 10-second destruction, RAM 3.2KB), retaining minimal anonymous physical delta logs without surveillance noise under soma-moa Charter 0.
* 60GHz FMCW Radar Angle Discrimination, 32x24 Thermal Matrix, and SCL Copper Foil Capacitive Fusion — Distinguishes 0-degree metallic specular reflections from 30–40 degree human body scattering angles, detects thermal differentials (36°C vs 20°C ambient), and tracks minute capacitive variations to eliminate sensing blind spots.
* Triple AND + eFPGA Ultra-Low Latency Physical Cutoff & Background AI Role Separation — 0.1ms ultra-low-latency drive cutoff is executed directly at the sensor triple AND and eFPGA hardware level, while local AI agents run background computations (several ms to tens of ms) to update risk weights and classify operation modes, preventing internal control logic contradictions while managing T-Reg 15% degraded mode.

---

## 2. Structural Limitations, Empirical Failure Modes, and Potential Operational Risk Analysis of Sheet Metal Machinery Pinch Accidents

### Official Machinery Pinch Point Classification by KOSA and OSHA 1910.212/217
Press brakes, shears, forming machines, bending machines, roll benders, pipe benders, notchers, ironworkers, and roll formers are designated as high-load pinch point, nip point, and Point of Operation hazard machinery, strictly requiring physical and electrical safeguards compliant with ANSI B11.3, ANSI B11.12, and OSHA regulations.

### Empirical Failure Mode 1 — Safeguard Bypass and Subsequent Accidents Caused by Alarm Fatigue During Under-10mm Micro-Cutting/Notching and Roller Feeder In-feed
During remnant trimming, small corner processing, or initial feeder in-feed on roll benders/roll formers, conventional single optical light curtains frequently misinterpret normal operator fingers or feed materials as hazards, causing nuisance trips. This leads operators to physically bypass or mask safeguards to perform manual work, resulting in repeated finger amputation and crushing accidents caused by unexpected strokes or roller intake.

### Empirical Failure Mode 2 — Gravity Free-Fall, Inertial Rotation During Abrupt Power Outages, and Unintended Auto-Restart Upon Power Restoration
Upon sudden power loss during press brake/ironworker operation, hydraulic pressure drop causes upper rams to free-fall due to gravity, or roll bender rollers to rotate via inertia. Upon power restoration, controller auto-restart configurations have caused severe accidents where operators cleaning or inspecting dies/rollers were struck or crushed.

### Empirical Failure Mode 3 — Entrapment/Pinch Accidents Driven by Fatigue and Accumulated Vibration/Impact During Continuous Rolling and Bending
During heavy sheet roll bending or continuous press shearing, strong mechanical impacts and rotational vibrations transfer to operator bodies, inducing musculoskeletal fatigue and loss of concentration. When sheet spring-back occurs, operators attempting to manually adjust materials without shutting off power frequently get pulled into rollers or dies.

### Potential Operational Adverse Effect Mitigation & Modern Safety Governance
This system functions as a silent auxiliary that provides a reassuring operational foundation through periodic safety posture validation rather than a surveillance tool. Following soma-moa philosophy, Heinrich's 1931 concept is modernized to Safety-II and Just Culture, flexibly supporting the continuity of normal operations rather than merely suppressing accidents, proactively mitigating safeguard tampering risks caused by surveillance pushback.

### Institutional Responsibility Escalation & Field Constraints
Under severe disaster prevention laws and OSHA General Duty clauses, pinch accident prevention is urgent; however, most industrial sites face significant operational downtime risks and financial burdens associated with replacing high-reliability equipment or modifying main PLC circuits.

---

## 3. Necessity of Local Computation and Edge Physical Control

### Non-Invasive Silent Auxiliary and Unused Terminal Interfacing
Compliant with IEC 60204-1 machine electrical equipment standards, lightweight independent modules interface directly with unused safety option terminals (X3/X4 spare slots), sniff existing light curtain OSSD photocouplers, or insert dry contacts in series with emergency stop loops without altering main PLC firmware, flexibly controlling enable signals (Motor EN / Relay) only during emergencies.

### Independent Safety Guarantee During Main Safeguard Bypass / Muting
Even when existing light curtains or interlock guards are manually bypassed or automatically muted for special processes, this non-invasive module operates independently from main PLC states, continuously enforcing cutoff control via triple-sensor fusion and eFPGA interlocks upon detecting physical worker hazard entry.

### Ultra-Low Latency Hardware Interlock & Local AI Role Separation
Emergency cutoff is executed at the local eFPGA hardware layer within 0.1ms, while a lightweight local AI (NPU) continuously updates contextual analysis and risk weightings in background pipelines to complement hardware interlock precision (aiming for IEC 61508/62061 functional safety).

### Power Outage Countermeasure: Normally De-Energized EPM/Mechanical Latch and Power Lockout (soma-moa L0/L1 Integration)
Upon main power loss, energy storage elements and normally de-energized electro-permanent magnets (EPM) or mechanical latches (spring-based fail-safe or pneumatic brakes) trigger immediately, physically attenuating and locking ram free-fall and roller rotation without drawing continuous power. Upon power restoration, soma-moa L2 FSM RECOVERY latch state is maintained, enforcing power lockout governance that prevents machine restart without manual operator re-authorization.

### Complex Sensor Fusion and Local Multimodal Analysis for False Positive Reduction
To overcome single-optical sensor vulnerabilities, 60GHz FMCW radar, 32x24 thermal cameras, copper foil capacitive sensors, and lightweight local vision/acoustic AI models operate simultaneously to precisely differentiate processing materials (sheet metal, pipes, structural steel) from human bodies.

### Air-Gapped and Offline Independent Operation
Operating with independent power and local processing units regardless of external network connectivity guarantees uninterrupted safety assistance even during communication loss or network failure.

---

## 4. 5mm Offset Auxiliary Finger, Immediate Origin/Reverse Recovery, and Quiet Assist Control Mechanism

### 5mm Offset Auxiliary Finger Structure
Auxiliary fingers with built-in 1.5T spring elasticity are positioned within 5mm of V-dies, shear blades, and roller inlets, fulfilling ISO 13857 and ISO 13854 clearance requirements by simultaneously providing physical support and pushing action to mitigate direct body access to hazard pinch zones.

### Quiet Assist Control for Under-10mm Manual Micro-Machining & Safeguard Bypass Response
During small piece cutting, corner notching, or remnant processing under 10mm where main safeguards are bypassed, Quiet Assist activates under Special-Purpose Tooling Mode. Triple sensors (36°C thermal differential, FMCW radar scattering angle, SCL capacitance) and lightweight AI track operator finger-to-workpiece distances at millimeter precision, triggering 0.1ms eFPGA motor stop and immediate origin ascent/reverse recovery only when fingers enter Point of Operation hazard zones.

### Smooth Deceleration Descent/Rotation, Ultra-Low Latency Cutoff, and Immediate Safety Height (Origin) Ascent / Reverse Recovery Logic
Interlocked with EN 12622 slow speed (Safe Speed ≤10mm/s and Mute Point) and ISO 13855 approach speed equations, any anomaly or unsafe posture detected during slow movement triggers immediate motor cutoff via triple AND + eFPGA within 0.1ms. The system immediately ramps up upper rams to preset safety heights or reverses roll bender rotation to mitigate secondary pinching.

* Physical Cushioning (Kinetic Energy Attenuation via Square Speed Ratio): Operating at Safe Speed (10mm/s) below Mute Point compared to top speed (200mm/s) reduces kinetic energy ($E_k = \frac{1}{2}m v^2$) to (10/200)^2 = 1/400. This prevents motor/hydraulic jamming, secures immediate ascent/reverse recovery torque, and mitigates secondary crushing and tooling damage.
* Psychological Cushioning: Predictable descent and rotation speeds suppress operator startle reflexes, preventing erratic sudden movements and assisting posture stability.
* Ergonomic Cushioning (Occupational Disease Prevention): Attenuates repeated mechanical impacts and rotational vibrations absorbed by operators during continuous work, protecting long-term worker health against musculoskeletal disorders.

### 5mm Proximity Bending/Forming/Rolling Exception Handling
Rejects indiscriminate shutdown within 5mm of V-dies or roller pinch points. As upper rams descend or rollers rotate, triple sensors evaluate whether operator hand postures represent safe support positioning (e.g., side support, feeding guides). Safe postures allow continuous processing, while posture breakdown triggers immediate ultra-low-latency stop and origin ascent/reverse recovery.

### Alarm Fatigue Mitigation & Tooling/Roller Geometry-Coupled Risk Rating Logic
Compliant with ANSI B11.3 and ANSI B11.12 risk assessment guidelines, evaluates upper/lower tooling profiles (gooseneck, offset), roller curvature/clearance, and stroke ranges to differentiate risk levels and prevent nuisance trips during non-hazardous operator positions. Suppressing false triggers keeps safety systems active (ON), preventing operator-initiated safeguard tampering.

### Dual-Operating Mode Governance (Normal Safety Mode vs. Special-Purpose Tooling Mode)
Separates control layers into two distinct operating modes regardless of production batch size:

* Normal Safety Mode — Active during standard sheet shearing, straight bending, and general punching operations, enforcing strict physical protection via triple-sensor fusion and triple AND eFPGA interlocks.
* Special-Purpose Tooling Mode — Active during non-standard/special tooling work (gooseneck, offset/angled blades), heavy sheet roll bending, pipe bending, under-10mm cutting/notching, or 5mm proximity bending. Accessible only via UWB smart tags/watch authentication or physical key switches, combining 5mm offset auxiliary fingers, T-Reg 15% power limitation, geometry-coupled risk weighting, independent auxiliary operation during main bypass, and immediate origin ascent/reverse recovery upon posture breakdown.

### soma-moa Charter 0 & Modernized Safety Framework (Safety-II & Just Culture) Integration
> soma-moa Charter 0 Axiom: "System governance is primary (Main), but functions as an auxiliary (Auxiliary) to human core operations."

* Safety-II Resilience (Hollnagel Resilience) — Focuses on supporting the continuity of overwhelming normal operations executed safely in the field rather than solely focusing on accident prevention, achieving safety and productivity simultaneously.
* Just Culture & PII Destruction Within 10 Seconds — Uses Heinrich's 300:29:1 ratio as a prevention motive while permanently purging routine movement and minor operator error logs from volatile memory buffers (RAM 3.2KB) within 10 seconds to prevent surveillance mistrust. Only critical hazard delta logs are stored locally in anonymous CBOR format.
* Silent Haptic Notifications — Replaces ambient loud alarms with private watch haptics (1 pulse for caution / 2 pulses for stop) to minimize alarm fatigue.

### Fail-Safe Defaults & Risk Assessment Conditions
Default settings strictly enforce Fail-Safe protection. Tooling/roller geometry exception weightings and Special-Purpose Tooling Mode activate only when accompanied by third-party verification compliant with ISO 13849/16092 and ANSI B11.19, official risk assessments, or administrator parameter approvals.

---

## 5. Overcoming Physical Constraints, Ultra-Low Latency Motor Stop, and T-Reg Governance

### eFPGA-Based Ultra-Low Latency Motor Stop Control
Upon hazard detection, hardware circuit logic controls motor enable signals directly within 0.1ms execution speeds without passing through software threads, inducing immediate drive cutoff and rotation stop.

### T-Reg 15% Fail-PRELOCK Mode
Upon entering boundary detection zones or triggering Special-Purpose Tooling Mode, machine output power is forcibly degraded to 15% to cushion abrupt mechanical impacts.

### HORIZONTAL_HANDOVER and 80% Proactive PRELOCK
Executes horizontal handovers between multiple operating zones (press lines, roller entry points, multi-point workstations), triggering proactive PRELOCK upon reaching 80% of hazard thresholds to suppress risk escalation.

### Anonymous Logging & PII Destruction Within 10 Seconds
Generates anonymized CBOR logs stripped of Personally Identifiable Information (PII) during events, permanently purging raw data within 10 seconds to maintain data privacy.

---

## 6. Industrial Segment Applications and Horizontal Deployment References

### Press & Shear Manufacturing Lines
Applied by mounting auxiliary fingers and triple-sensor edge modules on external bridge frames to prevent finger pinching in heavy sheet cutting and press forming lines.

### Heavy Roll Bending & Pipe Bending Processes
Places triple-sensor modules at 3-roll/4-roll bender and pipe bender feeder inlets for tank, piping, and curved sheet metal fabrication, triggering 0.1ms motor stop and immediate roller reversal upon hand entrapment risk.

### Notching, Ironworker, and Small Punching Processes
Equips non-invasive eFPGA auxiliary modules during multi-purpose shear/punch/notching work for under-10mm remnant cutting and corner trimming, providing quiet protection free of alarm fatigue.

### Continuous Roll Forming, Coil Slitting/Cut-to-Length, and Leveler Lines
Deploys edge AI and triple sensors at minute nip points along coil uncoiling, sheet levelers, continuous profile roll formers, and shear sections to mitigate pinch hazards on dual automated/manual lines.

### Small Press Brakes, Manual Micro-Cutting, and Legacy Equipment Processes
Non-invasively attaches lightweight edge AI terminals and eFPGA modules to legacy machinery without major modifications, assisting under-10mm manual cutting and fatigue risks through T-Reg performance degradation and ultra-low-latency motor cutoff.

### Smart Factory Safety Management Integration
Transfers anonymized safety cutoff and prevention logs processed at local terminals to central enterprise management systems (MES/S3) for integrated equipment safety history tracking.

---

## 7. Broad Concept Definitions: Communication, Transmission Media, Sensor Combination Variability, Tooling/Roller Scale, and Material Invariance

### Communication Protocol-Agnostic Standalone Operation
Completes safety control purely through internal independent sensor circuits and eFPGA hardware logic, regardless of wired/wireless network, Wi-Fi, Bluetooth, or Ethernet availability.

### Local AI Model & Sensor Media Agnosticism
Supports diverse neural network architectures for local AI (lightweight VLMs, CNN object detectors, acoustic anomaly detection, sLLMs) and flexibly extends across physical sensor media (next-gen radar, high-res thermal sensors, novel capacitive materials).

### Exemplary Nature and Dynamic Openness of Sensor Combinations
The triple-sensor configuration (FMCW radar, thermal imaging, capacitive sensing) serves merely as an illustrative embodiment. Dynamic additions, removals, replacements, or re-combinations of sensor media to maximize worker safety are fully encompassed within this prior-art scope.

### Single, Heterogeneous, and n+1 Multi-Sensor Combination Invariance ($n \ge 1$)
Unrestricted to specific sensor quantities; encompasses all physical and logical combinations of 1, 2, or $n+1$ heterogeneous sensors and modules ($n \ge 1$).

### Invariance to Tooling/Blade/Roller Size, Material Thickness, and Machining Dimensions
Fundamental safety control mechanisms—including triple-sensor fusion, 5mm offset auxiliary fingers, independent auxiliary operation during bypass, eFPGA ultra-low-latency motor cutoff, and immediate origin/reverse recovery—apply validly regardless of tooling sizes, stroke depths, bend radii, material thickness, or under-10mm micro-machining dimensions.

### Broad Concept Umbrella Declaration for Derivative Sheet Metal/Forming Machinery
All sheet metal and structural steel machinery employing these mechanisms—including roll benders, pipe/tube benders, notchers, ironworkers, roll formers, slitting/cut-to-length lines, sheet levelers, and crimping/riveting presses—are fully encompassed within this defensive prior-art whitepaper scope.

---

## 8. Practical Protection, License Separation, and Liability Disclaimer

### Original Language Supremacy Principle
Legal and technical interpretations of this specification strictly prioritize the Korean original (README.ko.md) as the governing text; translations in other languages serve informative reference purposes only.

### Dual Licensing Structure (CC BY 4.0 & Apache-2.0)
Textual expressions, documentation, and architecture blueprints in this repository are licensed under Creative Commons Attribution 4.0 International (CC BY 4.0), while derived code and executable implementations are dual-licensed under Apache License 2.0 (Apache-2.0), linked to the root LICENSE file (SPDX-License-Identifier: CC-BY-4.0 AND Apache-2.0). The legacy "DPL v1.0" notice was fully superseded by this standard dual licensing structure on September 27, 2026.

### Dynamic Account and Repository Transfer Flexibility Notice
All repositories within the soma-moa ecosystem may be freely transferred among associated individual and organizational accounts (deundeuni, deundeunilab, soma-moa) for governance, monitoring efficiency, and maintenance purposes. Legal prior-art status, copyright relationships, and technical connectivity remain fully preserved despite URL or namespace changes.

### Trade Secret Protection and Implementation Separation
This public whitepaper discloses top-level architectural concepts and mechanisms. Field calibration parameters (thresholds), eFPGA RTL schematics, precision CAD files, and production firmware binaries are maintained separately as confidential Trade Secrets. Proof-of-Concept (PoC) reference code is stored independently as an offline repository asset.

### Architect's Recommendation and Mandatory Safety Certification
Authored by the designer (deundeuni) to prevent high-risk sheet metal workplace accidents, this whitepaper serves as an engineering concept and defensive prior-art publication. Subsequent developers and commercializers are strongly recommended to obtain mandatory safety certifications (such as KCs, CE, UL, OSHA) in their respective jurisdictions. As a conceptual technical disclosure rather than a certified commercial product, legal safety certification, risk assessment, and functional safety (SIL/PL) verification duties belong entirely to the implementing party.

### Directional Guidance & AS-IS Non-Liability Disclaimer
Provides directional engineering concepts (AS-IS) for defensive publication without guaranteeing immediate physical completeness or prototype operation. The designer (deundeuni) assumes no legal liability for physical or property damages arising from implementations derived from this whitepaper. All engineering validation and safety assurance responsibilities reside with the party implementing and operating the equipment.

### Broad Concept Umbrella & n+1 Dynamic Sensor Combination Equivalent Expansion Declaration
All overarching concepts disclosed herein—including 5mm offset auxiliary fingers, Quiet Assist during under-10mm manual processing and safeguard bypass/muting, scale/thickness invariance, decelerated descent/rotation below Mute Point (kinetic energy attenuation $E_k \propto v^2$, startle reflex suppression, musculoskeletal disease prevention), ultra-low-latency cutoff/origin recovery, normally de-energized EPM/mechanical latch power loss response, 5mm proximity bending exception handling, geometry-coupled risk rating, dual-mode governance, soma-moa Charter 0 integration, PII 10s destruction, $n+1$ dynamic sensor combinations, eFPGA motor control, and T-Reg 15% degraded operation—are broadly encompassed for prior-art preemption.

### Design-to-Cost Flexibility & Customization
Hardware and layer structures represent optimal embodiments. Selective omissions, scaling, or custom optimizations based on market demand, cost efficiency, material thickness, operating conditions, and sensor counts ($n+1$) are recognized as functional equivalents within this prior-art scope.

### Non-Intentional Omission & Non-Exhaustive Disclaimer
Cited standards, principles, regulations, and codes serve as non-exhaustive examples. Unintentional omissions or missing references due to author constraints do not constitute intentional concealment; all derivative standards, revised codes, equivalent mechanisms, and sensor combinations connected to these concepts are included within this defensive publication scope.

### Defensive Publication and Prior Use Rights
Primarily published as defensive prior art to establish prior use rights under Article 103 of the Korean Patent Act and 35 U.S.C. §273, with independent design drawings, prototypes, and development logs maintained offline.

### Separation of Commercialization Details
Includes strictly pure open-source and prior-art disclosures; proprietary revenue models and commercial execution plans are managed in separate technical documentation.

---

## 9. Sources, References, and Patent Prior-Art DB Records

### Ecosystem Repositories
* Top-Level Universal Survival Architecture Master Hub (smart-system-multi-survival-architecture) — GitHub: deundeuni / smart-system-multi-survival-architecture
* Top-Level Gateway & Main Repository (soma-moa) — GitHub: soma-moa / soma-moa (Charter 0: Safety-II & Just Culture integration)
* Top-Level Universal Machine Tools Master Repository (Machine-Tools-Edge-Safety-Paper) — GitHub: deundeuni / Machine-Tools-Edge-Safety-Paper
* Stationary Machine Tools Sub-Whitepaper 1 (This Document) — GitHub: deundeuni / Press-Brake-Shear-Edge-Safety-Paper
* Stationary Machine Tools Sub-Whitepaper 2 (Lathe, Milling, Drill Press) — GitHub: deundeuni / Lathe-Milling-Drillpress-Edge-Safety-Paper
* Full-Stack Uninterruptible Emergency Power Survival Architecture Whitepaper (POWER_SURVIVAL_SPEC.ko.md) — soma-moa v1.0 Universal Emergency Power Survival Standard
* Account & Repository Namespace Transfer Flexibility — Recognizes transferability across deundeuni, deundeunilab, and soma-moa accounts while maintaining prior-art status and ecosystem interlocks regardless of path updates.

### Legal Statutes & Licenses
* Article 103 of the Korean Patent Act — Non-exclusive license based on prior use
* 35 U.S.C. §273 — Defense to Infringement Based on Prior Commercial Use
* Document Copyright: Creative Commons Attribution 4.0 International (CC BY 4.0)
* Code & Implementation License: Apache License 2.0 (Apache-2.0)

### Technical Reference Standards & Safety Codes
* ISO 12100 — Safety of machinery — General principles for design — Risk assessment and risk reduction
* ISO 13849-1 / ISO 13849-2 — Safety of machinery — Safety-related parts of control systems
* ISO 16092-1 / ISO 16092-2 — Machine tools safety — Presses — Safety requirement for mechanical / hydraulic presses
* IEC 61496-1 / IEC 61496-2 — Safety of machinery — Electro-sensitive protective equipment
* EN 12622:2009+A1:2013 — Safety of machine tools — Hydraulic press brakes (Basis for ≤10mm/s Safe Speed and Mute Point settings; analogously applied to roll benders/notchers/pipe benders)
* ANSI B11.3-2022 — Safety Requirements for Power Press Brakes
* ANSI B11.12 / ANSI B11.19 / ANSI B11.0 — Roll Bending & Forming Safeguarding / Performance Criteria for Safeguarding
* ISO 13855:2010 — Safety of machinery — Positioning of safeguards with respect to the approach speeds of parts of the human body
* ISO 13857:2019 — Safety of machinery — Safety distances to prevent hazard zones being reached by upper and lower limbs
* ISO 14119:2013 / ISO 14120:2015 / ISO 13850:2015 / ISO 13854 — Integrated safety interlocks, guard structures, emergency stop, and minimum gaps
* IEC 60204-1:2018 — Safety of machinery — Electrical equipment of machines (Basis for non-invasive X3/X4 slot and dry contact interfacing)
* IEC 61508 / IEC 62061 — Functional safety of electrical/electronic/programmable electronic safety-related systems (Basis for eFPGA SIL/PL functional safety)
* OSHA 1910.212 / OSHA 1910.217 — Machinery and Machine Guarding / Mechanical Power Presses
* KOSHA (Korea Occupational Safety and Health Agency) — Technical guidelines for press, shear, press brake, and roll bender pinch hazard prevention and safeguard installation

### Global Patent Prior-Art DB & Fork Point Mapping
* SICK AG Patent Family (DE 826131, US 3805060, DE 102013107696A1, etc.) — Autocollimator-based early photoelectric safety curtains and fixed beam muting. [Fork Point: Overcomes fixed light grid limits via 60GHz FMCW radar angle separation + thermal imaging 36°C differential + capacitive fusion, establishing an independent 'Quiet Assist' active during bypass/muting.]
* Lazer Safe Pty Ltd Patent Family (US 6525305B1, US 7298282B2, EP 1218153B1, etc.) — Press brake dynamic optical protection, RapidBend variable Mute Point, and PCSS-A embedded core logic. [Fork Point: Unlike systems requiring dedicated valve/hydraulic retrofits, interfaces non-invasively via IEC 60204-1 contact slots, 5mm offset spring-buffered fingers, normally de-energized EPM/mechanical latches, and eFPGA 0.1ms motor stop with origin/reverse recovery.]
* Fiessler Elektronik GmbH Patent Family (EP 0863802B1, US 6128938A, etc.) — AKAS press brake horizontal laser protection and upper ram coupling. [Fork Point: Prevents nuisance trips caused by upper punch laser scanning by dynamically weighting risks based on tooling/roller geometry and providing a dual Special-Purpose Tooling Mode for under-10mm micro-cutting.]
* Press Brake Safety Inc. / Boyer Patent Family (Reverse Flange Crush Zone Protection Patent, etc.) — Upper ram flange crush zone protection and variable light curtain mounts. [Fork Point: Extends beyond upper flange areas to all derivative sheet metal pinch points (roll benders, notchers, pipe benders) and couples speed-square kinetic energy attenuation below Mute Point to prevent musculoskeletal occupational diseases.]
* Inxpect S.p.A. Patent Family (WO 2019/081512A1, EP 3631521A1, etc.) — Industrial 60GHz FMCW radar SIL2/PLd volumetric radar safeguards. [Fork Point: Overcomes single-radar metallic specular noise by establishing 0-degree metallic vs. 30–40 degree human scattering angle discrimination coupled with thermal and copper foil capacitive 3-way AND fusion.]
* Pilz GmbH & Co. KG Patent Family (EP 3489569A1, DE 102017127546A1, etc.) — Industrial safety vision cameras and 3D relay spatial interlock controls. [Fork Point: Eliminates cloud/server latency and privacy leak concerns via edge-localized AI agents with 10-second PII destruction under Just Culture.]
* Siemens AG / Beckhoff Automation / Phoenix Contact Patent Family (EP 1852758B1, US 7836239B2, etc.) — FPGA-based hardware safety logic and ultra-low-latency emergency bus modules. [Fork Point: Replaces commercial PLC bus dependencies with independent localized eFPGA 0.1ms motor control, separating roles between hardware cutoff and background AI analysis while governing T-Reg 15% degraded mode.]

---

### Appendix A: Revision History
* v1.53 (2026-09-28) — Materialized Markdown heading symbols (##, ###) across all sections (1–9) and subsections to fully restore visual hierarchy during GitHub rendering.
* v1.52 (2026-09-28) — Officially added dynamic account/repository transfer flexibility clauses across Sections 8 and 9, cleaned up typos, and refined the soma-moa main repository path to the organizational account (soma-moa / soma-moa).
* v1.51 (2026-09-28) — Applied # H1 large title font, structured executive summaries with bullet points, and unified readability rules (horizontal rules, bolding, blockquotes, section consistency, numeric highlights) across Sections 1–9.
* v1.5 (2026-09-27) — Restructured licensing to standard dual-licensing (CC BY 4.0 & Apache-2.0) as of 2026-09-27, linked with root LICENSE file, officially replacing legacy DPL v1.0 notices.
* v1.4 (2026-09-23) — Integrated milestone release — Expanded scope to derivative sheet metal machinery, integrated global patent prior-art DB records and fork points, established 0.1ms eFPGA cutoff and background AI role separation, provided kinetic energy formula ($E_k \propto v^2$), and harmonized Safety-II/EPM/EN 12622 terminology.
* v1.3 (2026-09-21) — Declared sub-whitepaper status under Machine-Tools-Edge-Safety-Paper and reinforced $n+1$ dynamic sensor combination defense logic in Sections 6 and 7.
* v1.2 (2026-09-20) — Softened disclaimer tone (AS-IS) and synchronized master hub naming conventions.
* v1.1 (2026-09-20) — Strengthened commercialization recommendations, mandatory certification requirements (KCs, CE, UL), and legal disclaimers.
* v1.0 (2026-09-20) — Initial public disclosure — Proximity safety system and local AI edge autonomous survival control architecture specification.
