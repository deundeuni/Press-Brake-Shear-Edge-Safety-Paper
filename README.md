> **Original Authority Notice:** The supreme legal and engineering authority of this specification belongs to the original Korean text (`README.ko.md`). This file (`README.md`) serves solely as an auxiliary English reference. In case of any discrepancy, the Korean text shall prevail.  
> **국문 안내:** 본 문서는 영문 보조본입니다. 법적/기술적 원본 권위는 한글 `README.ko.md`에 있습니다.

# Press-Brake-Shear-Edge-Safety-Paper — Near-Proximity Safety System for Power Presses, Press Brakes, and Shears and Local AI Edge Autonomous Survival Control Architecture (v1.0 Core Baseline)

> It is hoped that this auxiliary safety system takes root not only in mobile transportation devices but across all industrial job sites, mitigating hand and finger injuries in high-difficulty metal fabrication workflows. Under the principle that safety cannot be compromised even on legacy equipment, this system does not force equipment replacement but aims to safely assist the operation of unique, long-established machinery. It avoids requiring replacement with newer models, thereby coexisting with legacy infrastructure through a lightweight structure focused on ultra-low latency execution.  
> This whitepaper was formulated based on a universal survival architecture independent of specific vendors or brands, prioritizing the creation of a safe working environment rather than worker surveillance. It integrates: 5mm offset auxiliary fingers compliant with EN 12622 (Safe Speed <= 10mm/s and Mute Point integration) and ISO 13857/13854 (reach prevention and minimum gaps); continuous silent auxiliary operation during manual/fine shearing under 10mm and safeguard bypass/muting; scale invariance across die sizes and material thicknesses; dynamic risk weighting based on die profile and gap clearance; smooth decelerated descent below Mute Point (mitigating inertial/hydraulic impact by 1/400, suppressing startle reflexes, and preventing musculoskeletal occupational illness from repetitive impacts); ultra-low latency motor stopping and immediate upward origin recovery; power-loss magnetic/mechanical drop prevention and auto-restart lockout (integrated with soma-moa emergency power survival); non-invasive dry contact integration via IEC 60204-1; eFPGA ultra-low latency motor control aligned with IEC 61508/62061 functional safety; Quiet Assist under the modern re-interpreted soma-moa safety framework (Safety-II operational continuity & Just Culture PII 10-second purge logging); 3-sensor fusion (60GHz FMCW radar, thermal array, capacitance); lightweight local multimodal AI analysis agents; T-Reg 15% power degradation mode; and UWB smart-tag authentication. Dual licensing is applied: CC BY 4.0 for text copyright and DPL v1.0 (Defensive Patent License v1.0) for derivative technical claims and patent immunity.

---

## 0. Designer's Declaration & Core Claims

1. **Architectural Conception:**  
   This architecture specification establishes an autonomous survival control structure designed to prevent worker entrapment hazards in heavy-duty machinery such as power presses, shears, and press brakes. It induces immediate motor cutoff at hardware (eFPGA) and lightweight local AI levels with ultra-low latency, operating independently of external communication networks or remote servers. The unified design authority of this architecture belongs exclusively to the designer (deundeuni).

2. **Software Utility Limitation:**  
   Tools utilized during the drafting of this document were limited to passive formatting and text refinement utilities operating under the explicit architectural logic and edge autonomous control boundaries defined by the designer.

3. **10 Core Mechanisms & Prior Art Fork Points:**  
   * 5mm Offset Auxiliary Finger Physical Structure — Incorporates a lightweight 1.5T spring-loaded 150/80mm structure operating within 5mm of the V-die, simultaneously performing physical support and push-away actions aligned with ISO 13857 and ISO 13854.  
   * Mute Point Slow-Descent, Ultra-Low Latency Stop, and Immediate Upward Origin Recovery Logic — Integrates with EN 12622 Safe Speed (<=10mm/s) and Mute Point profiles, mitigating inertial/hydraulic shock and bounce to prevent mechanical lockup while reducing worker startle reflexes and preventing long-term musculoskeletal occupational illness, triggering 0.1ms eFPGA motor cutoff and immediate upward recovery to safe origin height upon anomaly detection.  
   * Manual Shearing under 10mm and Safeguard Bypass/Muting Silent Auxiliary Continuity — Ensures that during small-component shearing or physical safeguard bypass/muting, the independent 3-sensor array and eFPGA interlock remain actively monitoring as a silent auxiliary guardian to execute ultra-low latency cutoffs.  
   * Power-Loss Magnetic/Mechanical Latching and Power-Restoration Auto-Restart Lockout — Employs electro-permanent magnetic (EPM) or mechanical brake latches to arrest gravity free-fall within 0.1ms during power cuts, retaining RECOVERY state upon power restoration to prevent unauthorized auto-restarts and unintended strokes (integrated with soma-moa power survival).  
   * 5mm Proximity Bending Exception-Handling Safety Assist — Avoids blanket shutdowns when operating within 5mm of the V-die, allowing continuous operation when 3-sensor fusion verifies safe holding postures while triggering immediate stops and upward recovery if posture deteriorates.  
   * Die Profile & Gap Dynamic Risk Weighting for Alarm Fatigue Mitigation — Dynamically weights hazard scores based on punch/die geometry and stroke gaps aligned with ANSI B11.3 and ISO 12100, suppressing nuisance trips when body parts are in safe clearance zones to encourage permanent safeguard activation.  
   * Dual Operating Mode Governance (Normal Safety Mode vs. Special-Purpose Tooling Mode) — Separates strict perimeter shutdown controls for standard jobs from UWB/physical-key authenticated special tooling modes for complex geometries, fine shearing under 10mm, or close-proximity bending, maintaining both efficiency and safety.  
   * Worker Assistance & Minimal PII 10s Purge Logging under soma-moa Charter #0 — Reinterprets Heinrich's 1931 philosophy through Safety-II (assisting 9,999 normal operational continuities) and Just Culture (purging PII in RAM within 10 seconds), preserving only anonymous physical delta logs.  
   * 60GHz FMCW Radar Scattering Angle Differentiation — Distinguishes 0-degree specular metallic reflections from 30–40 degree human body scattering angles in real time to reduce false alarms.  
   * 32x24 Thermal Array Matrix and SCL Capacitive Copper Fusion — Fuses thermal variance (human 36°C vs. sheet metal 20°C) with copper capacitive shift detection to eliminate sensor blind spots.

---

## 1. Structural Limitations, Failure Modes, and Operational Risks of Pinch Hazard Machinery

* **KOSHA & OSHA Official Machine Classifications** — Power presses, shearing machines, forming presses, and press brakes are officially designated as high-risk pinch point and Point of Operation hazard machinery requiring strict physical and electrical safeguards under ANSI B11.3 and OSHA 1910.212/217.  
* **Real-World Failure Mode 1: Nuisance Trips, Manual Bypass, and Fine Shearing Accidents** — Traditional optical guards frequently trigger false trips during non-standard tooling or fine shearing under 10mm. This leads operators to physically bypass or tape over optical sensors, resulting in severe finger amputation hazards when the machine cycles unexpectedly.  
* **Real-World Failure Mode 2: Power-Loss Free-Fall and Auto-Restart Entrapment** — Sudden power interruptions cause loss of hydraulic holding pressure, allowing heavy upper rams to free-fall. Furthermore, automatic controller restarts upon power restoration pose severe entrapment risks to workers inspecting die gaps.  
* **Real-World Failure Mode 3: Night Shift Fatigue, Cumulative Impact, and Entrapment** — Prolonged exposure to heavy mechanical shocks and fatigue during extended or night shifts reduces worker alertness, leading to entrapment when workers attempt to clear jammed workpieces without shutting down power.  
* **Operational Side-Effect Mitigation & Modern Governance** — Operating as a silent auxiliary rather than a surveillance tool, the system reinterprets Heinrich's ratio through Safety-II and Just Culture principles. It focuses on supporting 9,999 normal operational cycles, reducing worker resistance and preventing intentional safeguard disablement.  
* **Institutional Liability & Legacy Facility Limitations** — While expanded strict liability laws necessitate urgent entrapment prevention, most facilities face substantial financial and operational risks when forced to replace legacy machinery or overhaul main PLC logic.

---

## 2. Necessity of Edge/On-Device Local Computation and Local Physical Interlocks

* **Non-Invasive Silent Auxiliary and Unused Slot Interlocking (IEC 60204-1)** — Designed to avoid modifying main PLC logic or proprietary firmware, the system connects non-invasively via unused safety option terminals (X3/X4 slots), OSSD photocoupler tapping, or dry contacts in emergency stop loops.  
* **Independent Operation during Safeguard Bypass/Muting** — Even when main optical guards are muted or manually bypassed for special tooling or fine shearing, this independent edge module operates autonomously to maintain physical interlock protection.  
* **Ultra-Low Latency Hardware Interlock and Local AI Fusion (IEC 61508/62061)** — Evaluates sensor signals and AI inferences at local eFPGA hardware levels without cloud or network dependencies, achieving sub-millisecond execution.  
* **Power-Loss Mechanical Latching and Power Lockout (soma-moa L0/L1)** — Activates stored-energy mechanical/magnetic latches upon main power failure to arrest ram free-fall. Holds FSM RECOVERY state upon power restoration, requiring manual re-authentication before motion can resume.  
* **Multi-Sensor Fusion & Multimodal Noise Reduction** — Combines 60GHz FMCW radar, 32x24 thermal imaging, capacitive sensing, and local AI audio/vision analysis to reliably distinguish workpieces from human appendages.  
* **Air-Gapped Offline Autonomous Assurance** — Functions entirely offline, ensuring complete safety assistance even during total network or communication infrastructure failure.

---

## 3. 5mm Offset Auxiliary Finger, Immediate Upward Recovery, and Quiet Assist Control Mechanism

* **5mm Offset Auxiliary Finger Physical Structure** — Deploys 1.5T spring-loaded 150/80mm fingers within 5mm of the V-die, providing physical support and push-away buffering compliant with ISO 13857 and ISO 13854.  
* **10mm Manual Fine-Shearing Quiet Assist** — Tracks operator fingers during small-piece cutting or residual trimming down to 10mm. If fingers breach the Point of Operation, eFPGA motor shutdown and immediate upward ram recovery trigger within 0.1ms.  
* **Smooth Slow Descent, Ultra-Low Latency Stop, and Immediate Upward Recovery** — Synchronizes with EN 12622 Safe Speed (<=10mm/s) and Mute Point profiles to initiate ultra-low latency stops and immediate upward recovery upon hazard detection.  
  * **Physical Cushioning:** Decelerated descent below Mute Point reduces kinetic impact energy by 1/400 ($E_k = \frac{1}{2}mv^2$), eliminating mechanical bounce and hydraulic pressure surges to ensure immediate upward ram reversal without motor jamming.  
  * **Psychological Cushioning:** Predictable descent speeds suppress operator startle reflexes, preventing erratic panic movements.  
  * **Ergonomic Cushioning (Occupational Disease Prevention):** Dampens repetitive shock and vibration transmission to operators during long shifts, mitigating long-term musculoskeletal disorders.  
* **5mm Proximity Bending Exception Handling** — Evaluates hand postures via 3-sensor fusion during close-proximity bending, maintaining continuous operation for safe postures while triggering instant stops and recovery upon posture breakdown.  
* **Die Profile & Clearance Dynamic Risk Weighting** — Recognizes punch/die profiles (gooseneck, offset) and stroke gaps, adjusting risk thresholds to suppress false trips when hands are in non-hazardous clearance zones.  
* **Dual Operating Mode Governance** — Features Normal Safety Mode for standard bending and Special-Purpose Tooling Mode for complex dies or fine shearing, authenticated via UWB tags or physical keys.  
* **soma-moa Charter #0 & Safety-II / Just Culture Integration** — Adheres to the principle that system governance is primary while human work remains central. Purges raw data within 10 seconds (3.2KB RAM buffer) and utilizes silent haptic wristband alerts (1 pulse for caution, 2 for stop) to minimize alarm fatigue.  
* **Fail-Safe Default & Risk Assessment Pre-Conditions** — Retains strict Fail-Safe operation as default. Special tooling modes and exception weightings require prior risk assessment validation aligned with ISO 13849/16092 and ANSI B11.19.

---

## 4. Physical Constraints, Ultra-Low Latency Motor Stop, and T-Reg Governance

* **eFPGA Hardware-Level Motor Stop Control** — Bypasses software OS layers to directly control motor enable lines at the hardware circuit level, achieving 0.1ms execution speeds.  
* **T-Reg 15% Fail-PRELOCK Mode** — Restricts motor drive output to 15% power when entering hazard boundary zones or operating under special tooling modes to reduce impact forces.  
* **HORIZONTAL_HANDOVER and 80% Early PRELOCK** — Manages horizontal transition across multi-zone operations, triggering early PRELOCK at 80% risk thresholds.  
* **Anonymous Logging & 10s PII Purge** — Strips personally identifiable information, generating anonymous CBOR logs while permanently purging raw memory buffers within 10 seconds.

---

## 5. Industrial Field Segments and Horizontal Deployment References

* **Power Press & Shearing Manufacturing Lines** — Retrofits heavy plate shearing and press lines via external bridge modules housing auxiliary fingers and 3-sensor edge units.  
* **Small Press Brakes, Fine Shearing & Legacy Manual Machinery** — Installs non-invasively on manual or legacy press brakes without altering core machinery, assisting operators through T-Reg power degradation and low-latency stops.  
* **Smart Factory Integration** — Transmits anonymous safety event logs to central MES/S3 dashboards for facility-wide risk management.

---

## 6. Invariance over Communication, Sensing Media, Tooling Scale, and Material Thickness

* **Protocol-Agnostic Independent Operation** — Operates independently of wired/wireless networks, Wi-Fi, Bluetooth, or Ethernet protocols using dedicated internal sensor buses and eFPGA logic.  
* **Local AI Model & Sensing Media Invariance** — Accommodates lightweight VLM, CNN object detection, audio anomaly detection, or sLLM models across diverse physical media (radar, thermal, capacitive, optical).  
* **Tooling Scale, Material Thickness, and Cutting Dimension Invariance** — The core safety assistance mechanisms remain fully applicable regardless of variations in die dimensions, stroke depth, sheet metal thickness, or small cutting dimensions under 10mm.

---

## 7. Practical Protection & License Separation

* **Original Authority Principle:** The supreme legal and technical authority of this specification belongs to the original Korean text (`README.ko.md`). This file (`README.md`) serves solely as an auxiliary reference. In case of any discrepancy, the Korean text shall prevail.  
* **Dual Licensing Framework:** Creative Commons Attribution 4.0 International (**CC BY 4.0**) applies to text and visual expressions. The **Defensive Patent License v1.0 (DPL v1.0)** applies independently to technical ideas, architectural structures, and patent immunity claims.  
* **Trade Secret & Implementation Separation:** This document publishes high-level architectural concepts for prior art establishment. Precise field calibration parameters, eFPGA RTL source code, CAD schematics, and binary firmware are retained as protected Trade Secrets.  
* **Directional Guidance & No Implementation Warranty:** This specification provides conceptual architectural guidance for defensive prior art publication and does not guarantee commercial implementation or turn-key operation without site-specific engineering and safety validation.  
* **Comprehensive Prior Art Scope:** Covers all disclosed concepts including 5mm offset auxiliary fingers, 10mm fine-shearing silent assist during safeguard bypass/muting, scale/thickness invariance, smooth slow descent impact mitigation ($1/400$), occupational disease vibration dampening, ultra-low latency stops, immediate origin recovery, power-loss magnetic latching, auto-restart lockout, die dynamic weighting, dual-mode governance, soma-moa Charter #0 Safety-II/Just Culture integration, 3-sensor fusion, non-invasive dry contact interlocks, eFPGA control, T-Reg 15% degradation, and anonymous logging.  
* **Design-to-Cost Flexibility & Scaling Declaration:** Disclosed hardware structures represent optimal embodiments. Actual implementations allow selective omission, reduction, scaling, or custom optimization of specific modules based on market cost targets and field requirements while remaining within the prior art scope.  
* **Non-Intentional Omission & Non-Exhaustive Disclaimer:** Standards and codes cited herein serve as illustrative references. Any unintentional omission of related standards or equivalent technical principles does not constitute a waiver of prior art coverage over equivalent combinations.  
* **Defensive Publication & Prior Commercial Use Rights:** Primary publication establishes prior art under Korean Patent Act Art. 103 and US Patent Code 35 U.S.C. §273, supported by offline engineering records.  
* **Business Execution Plan Separation:** This open-source specification excludes commercial business plans, which are maintained in separate execution documents.

---

## 8. Sources & Records

* **Ecosystem Repositories & DOIs (Title-Kebab-Case Baseline)**  
  * Master Architecture Hub (`Smart-System-Multi-Survival-Architecture`) — GitHub: `deundeuni / Smart-System-Multi-Survival-Architecture`  
  * APU Survival Controller (`Chiplet-APU-Multi-System-Survival-Architecture`) — GitHub: `deundeuni / Chiplet-APU-Multi-System-Survival-Architecture` | CERN Zenodo DOI: `10.5281/zenodo.22374987`  
  * Strategy Specification (`ARCHITECTURE_STRATEGY.md`) — Subscribed within `Chiplet-APU-Multi-System-Survival-Architecture`  
  * Uninterrupted Power Survival Standard (`POWER_SURVIVAL_SPEC.ko.md`) — soma-moa v1.0 Universal Emergency Power Survival Standard  
  * Edge/On-Device Compute Paper (`On-Device-Edge-Survival-Paper`) — GitHub: `deundeuni / On-Device-Edge-Survival-Paper`  
  * Primary Specification Repository (`Press-Brake-Shear-Edge-Safety-Paper`) — GitHub: `deundeuni / Press-Brake-Shear-Edge-Safety-Paper` | Main Files: `README.md` (English Auxiliary) / `README.ko.md` (Korean Original)  
  * Gateway & Central Hub (`soma-moa`) — GitHub: `deundeuni / soma-moa` | CERN Zenodo DOI: `10.5281/zenodo.22435773` | Domain: `somamoa.ai.kr` | Philosophy Document: `PHILOSOPHY.ko.md` (soma-moa Charter #0, Section 4-4 Safety-II & Just Culture)  
* **Legal Statutes & Licenses**  
  * Korean Patent Act Article 103 — Prior Commercial Use Rights  
  * United States Code 35 U.S.C. §273 — Defense to Infringement Based on Prior Commercial Use  
  * Text Copyright: Creative Commons Attribution 4.0 International (CC BY 4.0)  
  * Patent Immunity: Defensive Patent License v1.0 (DPL v1.0)  
* **Technical Reference Standards & Safety Codes**  
  * ISO 12100 — Safety of machinery — General principles for design — Risk assessment and risk reduction  
  * ISO 13849-1 / ISO 13849-2 — Safety of machinery — Safety-related parts of control systems  
  * ISO 16092-1 / ISO 16092-2 — Machine tools safety — Presses — Mechanical / hydraulic press safety  
  * IEC 61496-1 / IEC 61496-2 — Safety of machinery — Electro-sensitive protective equipment  
  * EN 12622:2009+A1:2013 — Safety of machine tools — Hydraulic press brakes (Safe Speed <=10mm/s & Mute Point)  
  * ANSI B11.3-2022 — Safety Requirements for Power Press Brakes  
  * ANSI B11.19 / ANSI B11.0 — Performance Criteria for Safeguarding / Safety of Machinery  
  * ISO 13855:2010 — Positioning of safeguards with respect to approach speeds  
  * ISO 13857:2019 — Safety distances to prevent hazard zone access by upper/lower limbs  
  * ISO 14119:2013 / ISO 14120:2015 / ISO 13850:2015 / ISO 13854 — Interlocks, guards, E-stops, and minimum gaps  
  * IEC 60204-1:2018 — Safety of machinery — Electrical equipment of machines (Unused slot & dry contact interlocks)  
  * IEC 61508 / IEC 62061 — Functional safety of safety-related electrical/electronic control systems (SIL/PL eFPGA)  
  * OSHA 1910.212 / OSHA 1910.217 — General Duty & Mechanical Power Presses  
  * IEEE 446 / NFPA 110 — Emergency and Standby Power Systems  
  * KOSHA GUIDE — Korean Occupational Safety and Health Agency Press/Shear/Bending Guarding Technical Guidelines  

---

## Appendix A. Revision History

* **v1.0 (2026-09-20):** Initial Release — Unified Specification for Near-Proximity Safety System and Local AI Edge Autonomous Survival Architecture (`v1.0 Core Baseline`)
