> **Multilingual Publication Notice:** This document is a dual-language (Korean/English) publication of identical content. v1.2 2026-09-20 (Korean: [README.ko.md](README.ko.md))  
> **Original Authority Notice:** The ultimate criterion for legal and engineering judgment of this technical specification belongs to the Korean original (`README.ko.md`), and the English version functions solely as a supporting reference.

# Press-Brake-Shear-Edge-Safety-Paper — Press, Shear & Bending Machine Proximity Safety System and Local AI Edge Autonomous Survival Control Architecture (v1.2 Core Baseline)

> It is hoped that this safety auxiliary system will take root not only in mobile transport devices but throughout industrial sites, so that even one less person is injured in high-difficulty metalworking environments, often called the flower of sheet metal processing. Under the principle that safety cannot be compromised even for older equipment, this architecture does not force equipment replacement; rather, it aims to assist the safe operation of unique systems that each company has mastered over a long period. Since it does not premise replacement with a specific company's new models, it coexists with existing frameworks, focusing on a lightweight structure and ultra-low latency execution.  
> This white paper is formulated based on a universal survival architecture independent of specific corporations or brands, prioritizing the establishment of a safe auxiliary working environment over worker surveillance. It integrates and establishes: a 5mm offset auxiliary finger complying with EN 12622 (Safe Speed ≤ 10mm/s & Mute Point) and ISO 13857/13854 (preventing reach and minimum gaps); continuous Quiet Assist during manual micro-processing under 10mm or when existing safeguards are bypassed/muted; invariance to mold/blade scale and material thickness; risk weight calculation linked to blade/die profiles; Mute Point-linked decelerated descent (attenuating inertia/hydraulic shock by $1/400$, suppressing startle reflexes, and preventing musculoskeletal occupational diseases from long-term repetitive vibration) triggering ultra-low latency stop and immediate upward recovery to safety height (origin); non-powered mechanical/magnetic drop prevention and auto-restart prohibition during sudden power outages and recovery (linked to soma-moa emergency power survival); IEC 60204-1 based non-invasive contact interlocking; IEC 61508/62061 functional safety-oriented eFPGA ultra-low latency control; Quiet Assist linked to the soma-moa modern reinterpretation safety framework (Safety-II normal operation assist & Just Culture-based PII 10-second destruction minimal logging); triple sensor fusion (60GHz FMCW, thermal, capacitive); vision/thermal/anomalous sound lightweight local AI analysis agents; T-Reg 15% degraded performance mode; and UWB smart tag linked control. Text copyright applies CC BY 4.0, while derived technical claims and cross-licensing apply DPL v1.0 (Defensive Patent License v1.0) independently.

---

## 0. Designer's Declaration & Core Claims

1. **Architectural Conception & Uniqueness of Technology Combination:**  
   To prevent frequent worker accidents in high-load pinch-point hazard machinery such as presses, shears, and press brakes, this architectural specification establishes an autonomous survival control structure that immediately induces motor drive stoppage at ultra-low latency execution speeds at the terminal local hardware (eFPGA) and lightweight local AI level, without relying on communication networks or upper-level servers. The integrated design authority of this architecture belongs to the designer (deundeuni).

2. **Software Utility Limitation:**  
   The tools utilized during the drafting of this document were restricted to passive execution utilities that performed formatting and contextual refinement based on the architectural logic and edge autonomous control categories defined by the designer.

3. **Summary of Top 10 Core Mechanisms and Prior Art Fork Points:**  
   * 5mm Offset Auxiliary Finger Physical Structure — Encompasses a lightweight structure (150/80mm specification with 1.5T built-in spring) that simultaneously supports and pushes away within 5mm of the V-die, physically mitigating access to the pinch point in compliance with ISO 13857 and ISO 13854.  
   * Mute Point-Linked Decelerated Descent, Ultra-Low Latency Stop, and Immediate Upward Recovery Logic — Encompasses configurations linked to EN 12622 (Safe Speed ≤ 10mm/s and Mute Point profiles) to prevent mechanism offset during upward recovery via inertia/hydraulic shock and bounce suppression, while preventing worker startle reflexes and musculoskeletal occupational diseases. It induces 0.1ms eFPGA cutoff control and immediate upward recovery to the safety height (origin) upon detecting anomalies.  
   * Constant Quiet Assist Logic During Manual Processing (≤10mm) and Safeguard Bypass/Mute — Encompasses configurations performing continuous monitoring and ultra-low latency cutoff as a 'last line of quiet assist' via independent triple sensors and eFPGA hardware interlocks, even when existing optical sensors are physically bypassed for small micro-parts cutting.  
   * Non-Powered Magnetic/Mechanical Latch Against Sudden Power Outage and Auto-Restart Prohibition Logic — Encompasses soma-moa emergency power survival configurations that physically attenuate and fix the upper blade's free-fall (due to hydraulic/power loss) within 0.1ms via non-powered electromagnetic (EPM) or mechanical latches during sudden outages, maintaining the latch state (`RECOVERY`) upon power restoration to prevent unauthorized auto-restarts and unexpected strokes.  
   * 5mm Close-Proximity Bending Exception Handling Safety Assist — Encompasses configurations that avoid unconditional blanket cutoffs upon entering the 5mm V-die zone, maintaining operation if a safe posture is identified via triple sensors, but executing immediate stop and upward recovery if the posture deviates.  
   * Alarm Fatigue Prevention via Blade/Die Profile-Linked Risk Evaluation — Encompasses dynamic weighting configurations based on ANSI B11.3 and ISO 12100 that suppress unnecessary nuisance trips when the body is in a fixed safe clearance position not crossing the substantial pinch line given the mold profile and stroke gap, thereby encouraging the safety device to remain constantly active.  
   * Dual Operation Control Governance (Normal Safety Mode vs. Special-Purpose Tooling Mode) — Encompasses configurations separating strict safeguard modes for standard operations and UWB/physical key-authenticated special-purpose profile modes to simultaneously secure operational efficiency and protective reliability.  
   * Worker Assist & Minimal Logging Based on soma-moa Modern Reinterpretation Safety Framework — Encompasses configurations linked to the soma-moa Charter 0, modernizing Heinrich's philosophy (1931) with Safety-II (assisting 9,999 normal operation continuities) and Just Culture (PII 10-second destruction, RAM 3.2KB) to preserve only anonymous physical delta data without surveillance noise.  
   * Triple Sensor Fusion (60GHz FMCW Multiple Reflection Angle Distinction, 32x24 Thermal Matrix, SCL Copper Foil Capacitance) — Encompasses configurations compensating for blind spots by simultaneously distinguishing metal 0-degree reflections from human 30-40 degree scattering angles, detecting 36-degree vs. 20-degree thermal deviations, and sensing micro capacitance changes.  
   * Triple AND + eFPGA Ultra-Low Latency Motor Stop Control & T-Reg 15% Performance Degradation — Encompasses configurations satisfying IEC 61508 and IEC 62061 functional safety (SIL/PL) metrics by cross-verifying sensor signals and AI inferences via logic gates and eFPGA, stopping motor drive control at 0.1ms speeds and restricting output to 15%.

---

## 1. Structural Limits of Press/Shear Pinch Hazards, Real Failure Modes, and Operational Risk Analysis

* **Official Pinch Point Machinery Classification** — Presses, shears, forming machines, and press brakes are designated as representative high-load pinch point and Point of Operation hazard machines, strictly requiring physical and electrical safeguards complying with ANSI B11.3 and OSHA 1910.212/217.
* **Real Failure Mode 1: Accidents During Manual Processing After Temporary Optical Sensor Bypass** — When cutting micro-remnants under 10mm, conventional optical sensors often misjudge safe fingers as hazards, causing nuisance trips. This leads workers to physically bypass or mask the sensors, resulting in severe amputation accidents when the blade operates unexpectedly.
* **Real Failure Mode 2: Free Fall During Sudden Outages and Auto-Restart Malfunctions** — Momentary power outages can cause hydraulic pressure loss, leading the upper die to free-fall under its own weight. Furthermore, auto-restart settings upon power restoration have caused severe accidents while workers were cleaning or inspecting between molds.
* **Real Failure Mode 3: Entanglement Due to Night-Shift Fatigue and Long-Term Vibration** — Strong mechanical shocks and vibrations over long hours cause musculoskeletal fatigue and loss of concentration, frequently leading to entanglement accidents when workers attempt to clear jammed parts without cutting power.
* **Modern Safety Governance Application** — This system operates as a Silent Auxiliary, not a surveillance tool, assisting safe operation. It applies Safety-II and Just Culture to flexibly supplement 9,999 normal operations, mitigating the risk of safety device neutralization caused by field surveillance backlash.

---

## 2. Necessity of On-Device/Edge Computation and Local Physical Control

* **Non-Invasive Silent Auxiliary and Unused Terminal Integration** — In accordance with the IEC 60204-1 open standard, this lightweight independent module aims for a non-invasive structure by directly connecting to unused safety option terminals (X3/X4 slots), sniffing existing OSSD photocouplers, or inserting dry contacts in series within the emergency relay loop to flexibly control the motor EN/Relay only during emergencies.
* **Independent Safety Assist Guarantee During Safeguard Bypass/Mute** — Even if the main optical sensor or interlock guard is manually bypassed or auto-muted for special processes, this module operates independently of the main PLC, continuously performing cutoff control via triple sensor fusion and eFPGA interlocks upon detecting physical hazard entry.
* **Ultra-Low Latency Hardware Interlocks & Local AI Fusion** — Cross-verifies sensor signals and AI inference within local eFPGA circuits and lightweight NPU terminals to maximize physical execution speed without relying on upper clouds (Targeting IEC 61508/62061 functional safety).
* **Power-Lockout Governance (soma-moa L0/L1)** — EPM or mechanical air brake latches immediately actuate during power loss to physically arrest die free-fall. Upon power restoration, the soma-moa L2 FSM `RECOVERY` latch state is maintained, strictly prohibiting arbitrary machine restart without manual worker authentication (Power Lockout).
* **Air-Gap & Offline Autonomous Operation** — Driven by independent power and local compute units, fully maintaining safety auxiliary functions even in communication dead zones or network failure environments.

---

## 3. 5mm Offset Auxiliary Finger, Immediate Upward Recovery, and Quiet Assist Control Mechanisms

* **5mm Offset Auxiliary Finger Structure** — Deploys an auxiliary finger utilizing 1.5T spring elasticity within the 5mm V-die zone, complementing ISO 13857 and ISO 13854 clearance standards, physically supporting and pushing away body parts to mitigate direct entry paths into the hazardous mold zone.
* **Quiet Assist During 10mm Manual Micro-Processing and Safeguard Bypass** — Even when existing safeguards are bypassed, this system links with the Special-Purpose Tooling Mode. The triple sensors and lightweight AI track the distance between the worker's finger and the material at the millimeter level, triggering the 0.1ms eFPGA motor stop and immediate upward recovery *only* when a finger directly enters the Point of Operation, satisfying both process continuity and safety.
* **Mute Point Decelerated Descent, Ultra-Low Latency Stop, and Immediate Upward Recovery Logic** — Linked to EN 12622 (Safe Speed ≤ 10mm/s & Mute Point) and ISO 13855 approach speed formulas, it blocks motor drive via triple AND + eFPGA at 0.1ms upon detecting hazard signs during the decelerated descent phase. It immediately ramps up the upper die to a set safety height (origin or release height), fundamentally mitigating secondary pinch accidents caused by pressure inertia.
  * **Physical Buffer:** Decelerated descent below the Mute Point and T-Reg 15% limitation absorb inertia/hydraulic shock (kinetic energy attenuated by 1/400) and micro-bounce, preventing motor/hydraulic jams during sudden stops and securing upward recovery drive.
  * **Psychological Buffer:** Suppresses worker startle reflexes with predictable descent speeds.
  * **Ergonomic Buffer:** Flexibly attenuates long-term mechanical shocks and vibrations, preventing musculoskeletal occupational diseases.
* **5mm Close-Proximity Bending Exception Handling** — Eschews blanket cutoffs upon entering the 5mm V-die zone. The triple sensors determine in real-time whether the worker's hand posture is safe (side support, push-away posture). If safe, operation continues; if the posture collapses, immediate stop and upward recovery are executed.
* **Alarm Fatigue Mitigation & Profile-Linked Dynamic Risk Weighting** — Adhering to ANSI B11.3, it assesses risk by recognizing punch/die profiles (gooseneck, offset blades), clearance, and stroke range. By suppressing nuisance trips when the body is safely anchored outside the substantial pinch line, it encourages the safety device to remain constantly active (ON).
* **Dual Operation Control Governance**
  * **Normal Safety Mode:** Activated during standard flat iron and right-angle bending, performing strict physical protection via triple sensor fusion and eFPGA interlocks.
  * **Special-Purpose Tooling Mode:** Activated for non-standard molds, 10mm manual cuts, and 5mm close-proximity bending. Accessible only via UWB smart tag/security watch or physical key authentication, applying comprehensive exception handling and Quiet Assist.
* **soma-moa Charter 0 & Modern Reinterpretation Safety Framework (Safety-II & Just Culture)**
  * **Safety-II Resilience:** Focuses on assisting 9,999 normal operation continuities on-site, rather than merely suppressing accidents.
  * **Just Culture & PII 10-Second Destruction:** Routine operation and minor error logs are permanently destroyed from the volatile buffer (RAM 3.2KB) within 10 seconds to prevent surveillance backlash. Only critical hazard delta logs are saved locally in anonymous CBOR format.
  * **Quiet Haptic Alerts:** Utilizes security watch haptic notifications (1 vibration: caution / 2 vibrations: stop) recognizable only by the worker, minimizing fatigue from public noise alarms.
* **Fail-Safe Default & Risk Assessment Condition** — The default state maintains strict Fail-Safe protection. Special modes are governed to activate only after third-party verification, certified risk assessments, or strict administrator parameter approvals complying with ISO 13849/16092 and ANSI B11.19.

---

## 4. Physical Constraint Overcoming, Ultra-Low Latency Motor Stop, and T-Reg Governance

* **eFPGA-Based Ultra-Low Latency Motor Stop Control** — Directly controls the motor enable signal at the hardware circuit level without passing through software threads, inducing machine stop at 0.1ms speeds upon hazard detection.
* **T-Reg 15% Fail-PRELOCK Mode** — Forcibly degrades machine output to 15% upon entering sensor warning zones or during special-purpose modes to attenuate shocks from sudden operations.
* **HORIZONTAL_HANDOVER & 80% Pre-emptive Prelock** — Executes horizontal handover when moving between multiple work zones, triggering a pre-emptive prelock at 80% of the hazard threshold to suppress risk spread.
* **Anonymous Logging & PII 10-Second Destruction** — Generates anonymized logs in CBOR format excluding PII, permanently destroying raw data within 10 seconds of recording to maintain security.

---

## 5. Industrial Segment Applications & Horizontal Deployment References

* **Press & Shear Manufacturing Lines** — Applied as an external bridge-type module equipped with auxiliary fingers and triple sensors to prevent finger pinch accidents in large sheet metal cutting and press forming.
* **Small Bending Machines & Legacy Equipment** — Non-invasively attaches lightweight edge AI terminals and eFPGA modules without modifying existing equipment, assisting 10mm manual cutting and fatigue-related malfunction risks via T-Reg degradation and ultra-low latency motor stops.
* **Smart Factory Safety Integration** — Securely transfers anonymized safety cutoff and prevention logs processed at the terminal to the company's central management system (MES/S3).

---

## 6. Communication, Transport, Scale, and Material Thickness Agnostic Scope

* **Protocol-Agnostic Independent Operation** — Completes safety control solely with internal sensor circuits and eFPGA hardware logic, regardless of wireline/wireless networks, Wi-Fi, Bluetooth, or Ethernet availability.
* **Local AI Model & Sensor Media Agnosticism** — The local AI accommodates any neural network structure (VLM, CNN, audio anomaly detection, sLLM), and sensors broadly include next-gen radar, high-res thermal, and new material capacitive sensors.
* **Thickness & Scale Invariance** — Regardless of the overall size of press molds, bending blades/dies, shearing blades, stroke depth, sheet thickness, or geometric variations like 10mm micro manual cutting, the fundamental safety control mechanisms (triple sensor fusion, 5mm offset finger, independent assist during bypass, eFPGA 0.1ms stop, and upward recovery) apply validly and comprehensively.

---

## 7. Practical Protection, License Separation & Liability Disclaimer

* **Original Authority Rule:** The legal and technical interpretation of this specification prioritizes the Korean original (`README.ko.md`). Translations serve only for reference.
* **License Dual-Application:** Text copyright is licensed under **CC BY 4.0**, while technical concepts, architecture structures, defensive patent claims, and cross-licensing rights are independently licensed under **DPL v1.0**.
* **Trade Secret Separation:** This public white paper aims to disclose high-level architectural concepts. Actual calibration parameters, eFPGA RTL schematics, precise CAD files, and mass-production firmware binaries are kept separately as Trade Secrets. PoC reference codes are stored offline.
* **Architect's Recommendation & Mandatory Safety Certification:**  
  This white paper is an engineering conception formulated by the designer (deundeuni) to prevent accidents in high-difficulty metalworking sites. The designer strongly recommends that all subsequent developers and businesses intending to manufacture or implement actual devices based on this architecture strictly obtain mandatory legal safety certifications (KCs, CE, UL, OSHA, etc.) for safe commercialization. However, as this white paper is a conceptual technical disclosure and not a certified end-product, the obligations for legal safety certification, risk assessment, and functional safety (SIL/PL) verification during the implementation process belong entirely to the 'actual implementing and operating entity'.
* **Directional Guidance & AS-IS Non-Liability Disclaimer:**  
  This white paper serves solely for prior art defensive publication and directional guidance. It does not directly guarantee physical completeness, prototype operation, or commercial deployment (provided "AS-IS"). The author and designer (deundeuni) shall not bear any legal liability (civil or criminal) for unexpected physical injuries, property losses, or legal penalties resulting from devices manufactured or operated using the logic disclosed herein. All engineering verification and safety liabilities upon field application rest entirely with the implementing and operating entities.
* **Scope Inclusion:** All high-level concepts described herein—including the 5mm offset auxiliary finger, continuous Quiet Assist during safeguard bypass, scale/thickness invariance, Mute Point decelerated descent (inertia attenuation/startle suppression/occupational disease prevention) and immediate upward recovery logic, power-lockout/latch logic during outages, 5mm close-proximity exception handling, profile-linked risk weighting for alarm fatigue, dual operation modes, soma-moa Charter 0 (Safety-II/Just Culture) PII destruction logging, triple sensor fusion, non-invasive local AI agents, eFPGA motor control, T-Reg 15%, HORIZONTAL_HANDOVER, UWB authentication, and unused terminal integration—are broadly embraced as prior art.
* **Design-to-Cost Flexibility:** Hardware configurations and layer structures represent optimal embodiments. Depending on market demand, economy, and operating conditions, selective omission, scaling, or custom optimization of specific modules is flexibly permitted and falls within the scope of this prior art disclosure.
* **Non-Intentional Omission & Non-Exhaustive Disclaimer:** Cited standards, principles, and laws are illustrative and not exhaustively limiting. Omissions due to subjective limits do not constitute intentional exclusion. All derivative standards and equivalent combinations linked to the disclosed high-level concepts are deemed included.
* **Defensive Publication & Prior Commercial Use:** Published primarily as defensive prior art, maintaining offline design logs to establish prior use rights under ROK Patent Act Art. 103 and US 35 U.S.C. §273.
* **Commercialization Separation:** Commercialization execution plans are managed in separate technical documents.

---

## 8. Sources & Records

* **Ecosystem Repositories & DOIs**
  * Top-Level Universal Survival Architecture Master Hub (`smart-system-multi-survival-architecture`) — GitHub: `deundeuni / smart-system-multi-survival-architecture`
  * High-Level Universal Survival Architecture & APU Computational Controller (`chiplet-apu-multi-system-survival-architecture`) — GitHub: `deundeuni / chiplet-apu-multi-system-survival-architecture` | CERN Zenodo DOI: `10.5281/zenodo.22374987`
  * High-Level Architecture Strategy Specification (`ARCHITECTURE_STRATEGY.md`) — Included in `chiplet-apu-multi-system-survival-architecture`
  * Full-Stack Zero-Downtime Emergency Power Survival Architecture White Paper (`POWER_SURVIVAL_SPEC.ko.md`) — soma-moa v1.0 Universal Emergency Power Survival Standard
  * On-Device Edge Autonomous Computation White Paper (`On-Device-Edge-Survival-Paper`) — GitHub: `deundeuni / On-Device-Edge-Survival-Paper`
  * Dedicated Repository for this White Paper (`Press-Brake-Shear-Edge-Safety-Paper`) — GitHub: `deundeuni / Press-Brake-Shear-Edge-Safety-Paper` | Main Files: `README.md` (English Aux) / `README.ko.md` (Korean Original)
  * Top-Level Hub Gateway & Main Repository (`soma-moa`) — GitHub: `deundeuni / soma-moa` | CERN Zenodo DOI: `10.5281/zenodo.22435773` | Domain: `somamoa.ai.kr` | Core Philosophy: `PHILOSOPHY.ko.md` (soma-moa Charter 0, Ch 4-4 Heinrich 1931 Reinterpretation & Safety-II / Just Culture / Quiet Assist)
* **Legal Statutes & Licenses**
  * ROK Patent Act Article 103 — Non-exclusive license based on prior use
  * US Patent Law 35 U.S.C. §273 — Defense to Infringement Based on Prior Commercial Use
  * Document Copyright: Creative Commons Attribution 4.0 International (CC BY 4.0)
  * Patent Defense & Practice License: Defensive Patent License v1.0 (DPL v1.0)
* **Technical Reference Standards & Safety Codes**
  * ISO 12100 — Safety of machinery — General principles for design — Risk assessment and risk reduction
  * ISO 13849-1 / ISO 13849-2 — Safety of machinery — Safety-related parts of control systems
  * ISO 16092-1 / ISO 16092-2 — Machine tools safety — Presses — Safety requirement for mechanical / hydraulic presses
  * IEC 61496-1 / IEC 61496-2 — Safety of machinery — Electro-sensitive protective equipment
  * EN 12622:2009+A1:2013 — Safety of machine tools — Hydraulic press brakes (Basis for Safe Speed ≤ 10mm/s & Mute Point settings)
  * ANSI B11.3-2022 — Safety Requirements for Power Press Brakes (US technical standard for Point of Operation guarding)
  * ANSI B11.19 / ANSI B11.0 — Performance Criteria for Safeguarding / Safety of Machinery
  * ISO 13855:2010 — Safety of machinery — Positioning of safeguards with respect to the approach speeds of parts of the human body
  * ISO 13857:2019 — Safety of machinery — Safety distances to prevent hazard zones being reached by upper and lower limbs (Basis for 5mm physical mitigation)
  * ISO 14119:2013 / ISO 14120:2015 / ISO 13850:2015 / ISO 13854 — Safety interlocks, guard structures, emergency stop, and minimum gaps integration standards
  * IEC 60204-1:2018 — Safety of machinery — Electrical equipment of machines (Basis for unused X3/X4 slot and dry contact integration)
  * IEC 61508 / IEC 62061 — Functional safety of electrical/electronic/programmable electronic safety-related systems (SIL/PL functional safety basis for eFPGA logic)
  * OSHA 1910.212 / OSHA 1910.217 — Machinery and Machine Guarding / Mechanical Power Presses
  * IEEE 446 / NFPA 110 — Emergency and Standby Power Systems for Industrial Applications
  * KOSHA GUIDE — Technical guidelines for preventing pinch point accidents in presses, shears, and bending machines.

---

## Appendix A. Revision History

* **v1.2 (2026-09-20):** Softened liability disclaimer tone (AS-IS basis) and reverted master hub repository naming to lowercase kebab-case (`v1.2 Core Baseline`)
* **v1.1 (2026-09-20):** Added commercialization recommendation, reinforced mandatory legal safety certification compliance, and clarified absolute liability disclaimer
* **v1.0 (2026-09-20):** Initial Release — Integration of Pinch-Point Machinery Proximity Safety System and Local AI Edge Autonomous Survival Control Architecture
