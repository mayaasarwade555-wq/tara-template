# TARA — Threat Analysis & Risk Assessment Template
### Aligned with ISO/SAE 21434 Clause 15

> Created by Maya Sarwade | Cybersecurity PM | FEV India  
> Based on real-world TARA experience across automotive OEM programs

---

## What is TARA?

**Threat Analysis and Risk Assessment (TARA)** is a structured methodology defined in **ISO/SAE 21434 Clause 15** to identify cybersecurity threats to a vehicle or component, assess their risk, and determine appropriate treatment actions.

TARA is the foundation of every automotive cybersecurity program. Without it, you cannot define cybersecurity goals, requirements, or test cases.

---

## TARA Process Overview

```
Step 1: Define Item & Scope
        ↓
Step 2: Asset Identification
        ↓
Step 3: Threat Scenario Identification
        ↓
Step 4: Impact Rating (Safety / Financial / Operational / Privacy)
        ↓
Step 5: Attack Path Analysis
        ↓
Step 6: Attack Feasibility Rating
        ↓
Step 7: Risk Value Determination
        ↓
Step 8: Risk Treatment Decision
        ↓
Step 9: Cybersecurity Goals Definition
```

---

## Step 1 — Item Definition & Scope

| Field | Description |
|-------|-------------|
| Item Name | e.g., Telematics Control Unit (TCU) |
| Item Version | e.g., v2.1 |
| Vehicle Program | e.g., SUV Platform — Model Year 2026 |
| TARA Author | Name + Role |
| TARA Date | DD/MM/YYYY |
| Review Date | DD/MM/YYYY |
| Related Standards | ISO/SAE 21434, UNECE R155, AIS 189 |

**Item Description:**
> Describe the item's function, interfaces, and operational environment in 3–5 sentences.

**Item Boundary:**
> Define what is IN scope and OUT of scope for this TARA.

---

## Step 2 — Asset Identification

Assets are data, functions, or resources that have value and must be protected.

| Asset ID | Asset Name | Asset Type | Description | Cybersecurity Property |
|----------|-----------|------------|-------------|----------------------|
| AST-001 | Vehicle Speed Data | Data | Real-time vehicle speed transmitted via CAN bus | Integrity, Availability |
| AST-002 | OTA Update Package | Software | Firmware update delivered via cellular network | Authenticity, Integrity |
| AST-003 | Remote Access Function | Function | Allows remote lock/unlock via mobile app | Authenticity, Authorization |
| AST-004 | Driver Personal Data | Data | Driver profiles stored in infotainment system | Confidentiality, Privacy |
| AST-005 | Diagnostic Access | Function | OBD-II diagnostic interface | Authorization, Integrity |

**Cybersecurity Properties (CIA+):**
- **Confidentiality** — Protecting data from unauthorised disclosure
- **Integrity** — Ensuring data/function is not tampered with
- **Availability** — Ensuring function is available when needed
- **Authenticity** — Ensuring identity of communicating parties

---

## Step 3 — Threat Scenario Identification

For each asset, identify realistic threat scenarios using the **STRIDE** model.

| Threat ID | Asset ID | Threat Category | Threat Scenario | Attacker Goal |
|-----------|----------|----------------|----------------|---------------|
| THR-001 | AST-001 | Tampering | Attacker injects false speed data via CAN bus | Cause accident / disable safety systems |
| THR-002 | AST-002 | Spoofing | Attacker delivers malicious OTA update | Gain persistent control of ECU |
| THR-003 | AST-003 | Elevation of Privilege | Attacker clones legitimate mobile app token | Unauthorised remote vehicle access |
| THR-004 | AST-004 | Information Disclosure | Attacker extracts driver PII from infotainment | Privacy violation / data sale |
| THR-005 | AST-005 | Tampering | Attacker modifies ECU via OBD-II port | Disable safety functions |

**STRIDE Model:**
- **S**poofing — Impersonating something or someone
- **T**ampering — Modifying data or code
- **R**epudiation — Denying an action occurred
- **I**nformation Disclosure — Exposing data to unauthorised parties
- **D**enial of Service — Preventing legitimate access
- **E**levation of Privilege — Gaining unauthorised capabilities

---

## Step 4 — Impact Rating

Rate the potential impact of each threat scenario across four dimensions.

**Impact Categories:**

| Category | Severe (3) | Major (2) | Moderate (1) | Negligible (0) |
|----------|-----------|-----------|--------------|----------------|
| **Safety** | Life-threatening injuries or fatalities | Serious injuries | Minor injuries | No injuries |
| **Financial** | > €10M loss | €1M–€10M loss | €10K–€1M loss | < €10K loss |
| **Operational** | Complete loss of vehicle function | Major function degraded | Minor function degraded | Negligible |
| **Privacy** | Mass PII exposure / regulatory breach | Sensitive data of many users | Personal data of few users | Non-personal data |

**Impact Assessment Table:**

| Threat ID | Safety Impact | Financial Impact | Operational Impact | Privacy Impact | Overall Impact |
|-----------|--------------|-----------------|-------------------|----------------|----------------|
| THR-001 | Severe (3) | Major (2) | Severe (3) | Negligible (0) | **Severe** |
| THR-002 | Major (2) | Major (2) | Severe (3) | Moderate (1) | **Severe** |
| THR-003 | Moderate (1) | Moderate (1) | Major (2) | Moderate (1) | **Major** |
| THR-004 | Negligible (0) | Moderate (1) | Negligible (0) | Severe (3) | **Major** |
| THR-005 | Severe (3) | Major (2) | Severe (3) | Negligible (0) | **Severe** |

---

## Step 5 — Attack Path Analysis

Identify realistic attack paths an attacker could use to realise the threat scenario.

| Threat ID | Attack Path ID | Attack Path Description | Entry Point | Prerequisites |
|-----------|---------------|------------------------|-------------|---------------|
| THR-001 | AP-001 | Physical access to OBD port → CAN bus injection | OBD-II Port | Physical vehicle access |
| THR-002 | AP-002 | Man-in-the-middle on cellular network → malicious package delivery | Cellular interface | Network interception capability |
| THR-003 | AP-003 | Reverse engineering mobile app → extract auth token → replay attack | Mobile app | App decompilation skills |
| THR-004 | AP-004 | Physical access to infotainment → data extraction via USB | USB port | Physical access + forensic tools |
| THR-005 | AP-005 | Aftermarket OBD dongle with custom firmware → ECU write commands | OBD-II Port | Aftermarket hardware |

---

## Step 6 — Attack Feasibility Rating

Rate how feasible it is for an attacker to successfully execute the attack path.

**Feasibility Factors (ISO/SAE 21434 Annex B):**

| Factor | Low (1) | Medium (2) | High (3) |
|--------|---------|-----------|---------|
| **Elapsed Time** | > 6 months | 1 week – 6 months | < 1 week |
| **Specialist Expertise** | Expert knowledge required | Specialised knowledge | Standard knowledge |
| **Knowledge of Item** | Not publicly known | Restricted | Public |
| **Window of Opportunity** | Difficult / limited access | Moderate access | Easy / unlimited |
| **Equipment** | Bespoke / expensive | Specialised | Standard |

**Feasibility Assessment:**

| Threat ID | Attack Path | Elapsed Time | Expertise | Knowledge | Opportunity | Equipment | Feasibility Score | Feasibility Level |
|-----------|------------|-------------|-----------|-----------|-------------|-----------|------------------|------------------|
| THR-001 | AP-001 | Low (1) | Low (1) | Medium (2) | High (3) | Low (1) | 8 | **Medium** |
| THR-002 | AP-002 | Medium (2) | High (3) | Low (1) | Medium (2) | Medium (2) | 10 | **High** |
| THR-003 | AP-003 | Medium (2) | Medium (2) | Medium (2) | High (3) | Low (1) | 10 | **High** |
| THR-004 | AP-004 | Low (1) | Low (1) | Low (1) | Medium (2) | Low (1) | 6 | **Low** |
| THR-005 | AP-005 | Low (1) | Medium (2) | High (3) | High (3) | Medium (2) | 11 | **High** |

*Score ≤ 6: Low | 7–10: Medium | 11–13: High | 14–15: Very High*

---

## Step 7 — Risk Value Determination

Combine Impact and Feasibility to determine the overall Risk Value.

**Risk Matrix:**

| | Negligible Impact | Moderate Impact | Major Impact | Severe Impact |
|-|------------------|----------------|-------------|--------------|
| **High Feasibility** | Low Risk | Medium Risk | High Risk | **Critical Risk** |
| **Medium Feasibility** | Low Risk | Low Risk | Medium Risk | **High Risk** |
| **Low Feasibility** | Negligible | Low Risk | Low Risk | **Medium Risk** |

**Risk Value Table:**

| Threat ID | Impact Level | Feasibility Level | Risk Value | Risk Level |
|-----------|-------------|------------------|------------|------------|
| THR-001 | Severe | Medium | 6 | **High** |
| THR-002 | Severe | High | 9 | **Critical** |
| THR-003 | Major | High | 6 | **High** |
| THR-004 | Major | Low | 2 | **Low** |
| THR-005 | Severe | High | 9 | **Critical** |

---

## Step 8 — Risk Treatment Decision

For each risk, decide the treatment approach.

**Treatment Options:**
- **Avoid** — Remove the asset or function
- **Reduce** — Implement cybersecurity controls to lower risk
- **Share** — Transfer risk to supplier or insurer
- **Accept** — Accept residual risk (document rationale)

| Threat ID | Risk Level | Treatment Decision | Cybersecurity Control | Residual Risk | Owner |
|-----------|------------|-------------------|----------------------|---------------|-------|
| THR-001 | High | Reduce | CAN bus message authentication (MAC) | Low | ECU Team |
| THR-002 | Critical | Reduce | Code signing for OTA packages + certificate pinning | Medium | Connectivity Team |
| THR-003 | High | Reduce | Token expiry + multi-factor authentication | Low | App Team |
| THR-004 | Low | Accept | Existing data encryption sufficient | Low | Infotainment Team |
| THR-005 | Critical | Reduce | Disable diagnostic write access in production mode | Low | ECU Team |

---

## Step 9 — Cybersecurity Goals

Define high-level cybersecurity goals derived from risk treatment decisions.

| Goal ID | Cybersecurity Goal | Related Threat | CAL Level | Verification Method |
|---------|--------------------|---------------|-----------|-------------------|
| CG-001 | The TCU shall authenticate all CAN bus messages using MAC to prevent injection attacks | THR-001 | CAL 3 | Penetration testing |
| CG-002 | The OTA system shall verify package authenticity via code signing before installation | THR-002 | CAL 4 | Code review + pen test |
| CG-003 | The remote access system shall enforce token expiry and MFA | THR-003 | CAL 3 | Security testing |
| CG-004 | Diagnostic write access shall be disabled in production ECU configuration | THR-005 | CAL 4 | Configuration audit |

**CAL = Cybersecurity Assurance Level (CAL 1–4, per ISO/SAE 21434)**

---

## TARA Review & Approval

| Role | Name | Signature | Date |
|------|------|-----------|------|
| TARA Author | | | |
| Cybersecurity Manager | | | |
| System Architect | | | |
| Quality Manager | | | |

---

## Document Control

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | | Maya Sarwade | Initial release |
| | | | |

---

**Author:** Maya Sarwade | Cybersecurity PM | [LinkedIn](https://linkedin.com/in/mayasarwade) | sarawademaya@gmail.com  
*This template is shared for educational purposes based on ISO/SAE 21434 methodology.*
# tara-template
