---
title: IRP-04 — Third-Party AI Serious Malfunction, Bias Spike & GenAI DLP Breach Playbook
---

# IRP-04: Third-Party AI Serious Malfunction, Bias Spike & GenAI DLP Breach
**Playbook ID:** `IRP-04` · **Primary Pillar:** Pillar 3 & Pillar 6 · **Linked Registers:** [`pillar-03-dora-incident-cbi-clock.xlsx`](../pillar-03-dora-incident-cbi-clock.xlsx) & [`pillar-06-eu-ai-act-inventory-and-fria.xlsx`](../../pillar-06-eu-ai-act-governance/pillar-06-eu-ai-act-inventory-and-fria.xlsx)

---

## 1. Trigger & Severity Classification (`T+0`)

### Activation Triggers
Activate `IRP-04` immediately upon any of the following telemetry, compliance, or vendor alerts across deployed third-party AI systems (`AI-001` through `AI-006`):
* **Fraud / AML AI False-Positive Spike (`AI-001` / `AI-005`):** Third-party fraud or sanctions API begins falsely blocking `> 10%` of legitimate SEPA Instant (`CIBS-01`) or card authorization (`CIBS-02`) traffic, threatening Board Impact Tolerances (`30m` / `45m`).
* **High-Risk AI Discrimination / Malfunction (`AI-002` Underwriting / `AI-004` Biometric eKYC):** Automated monitoring or vendor advisory detects a sudden demographic false-rejection disparity (`> 3%`), broken `SHAP`/reason-code outputs, or failure of human-in-the-loop override queues (`Art. 26(5)`).
* **Customer Chatbot Hallucination / Unauthorized Disclosure (`AI-003`):** Customer support LLM fabricates binding financial/fee commitments, suffers prompt-injection bypass, or leaks another customer's session context.
* **GenAI Egress DLP / Shadow AI Breach (`AI-006` / `GEN-01`–`GEN-04`):** Egress proxy or CASB detects raw card `PAN` or customer `PII` transmitted to an external LLM endpoint without redaction or Zero-Data-Retention (`ZDR`) protection.

### Dual Statutory Regime (`DORA` + `EU AI Act / Irish AI Act 2026`)
Because the **Central Bank of Ireland (CBI)** is both the prudential/DORA supervisor and the designated AI market surveillance authority under **Ireland's Regulation of Artificial Intelligence Act 2026**, a serious AI malfunction triggers **parallel statutory duties**:
1. **EU AI Act `Article 26(5)` (Deployer Duty):** Duty to immediately suspend use of a high-risk AI system presenting a serious risk and notify the third-party **Provider** and the **CBI**.
2. **DORA `Article 19` & `RTS 2024/1772`:** Major ICT-related incident reporting (`4-hour` Initial Notice) if the AI API disruption degrades `CIBS-01`–`CIBS-05` or breaches data confidentiality.

---

## 2. Out-of-Band Command & Roles (`T+0 to T+15 Mins`)

| Crisis Role | Designated Owner | Primary Responsibility During `IRP-04` |
| :--- | :--- | :--- |
| **AI & ICT Risk Lead** | Head of ICT & InfoSec Risk | Authorises immediate **60-second API kill-switch**, runs **45-min DORA triage**, and coordinates vendor escalation. |
| **Accountable PCF Owner** | `PCF-52` (MLRO) or `CRO` (`PCF-14`) | Holds statutory accountability for the affected AI system (`AI-001/004/005` = MLRO; `AI-002` = CRO) and approves fallback rules. |
| **Platform & API Engineering Lead** | Principal Payments / API Engineer | Executes feature-flag kill-switch, switches traffic to deterministic rules engine, and preserves inference logs (`Art. 26(6)`). |
| **Data Protection & Legal Lead** | DPO & Head of Compliance (`PCF-52`) | Evaluates `PII`/`PAN` exposure for GDPR `Art. 33` (DPC) and files `EU AI Act Art. 26(5)` / `DORA Art. 19` CBI notices. |

* **Command Bridge:** Open `#inc-ai-governance-alert` in Slack Enterprise Grid + PagerDuty Bridge.

---

## 3. Immediate Containment: The 60-Second API Kill-Switch (`T+0 to T+30 Mins`)

1. **Execute Feature-Flag API Kill-Switch (`<= 60 Seconds`):**
   * Engineering toggles the production feature flag in the API Gateway to bypass the malfunctioning third-party AI endpoint immediately:
     * **`AI-001` (Fraud Scoring) / `AI-005` (AML Screening):** Fail over automatically to the **in-house deterministic rules engine** (velocity, geo-IP, and exact sanctions list matching) so SEPA Instant (`CIBS-01`) and card rails (`CIBS-02`) continue processing within the `30-minute` Impact Tolerance.
     * **`AI-002` (Merchant Underwriting) / `AI-004` (Biometric eKYC):** Route 100% of pending applications to the **manual human underwriter / AML document review queue** (`Pillar 6` human oversight fallback).
     * **`AI-003` (Customer Support Chatbot):** Disable the chat widget immediately and route users to Dublin live support agents.
2. **Revoke Egress Tokens & Block Shadow AI (`DLP Breach`):**
   * If raw `PAN` or `PII` leaked to an external LLM (`GEN-01`–`GEN-04`), immediately revoke the outbound API key, block the destination domain at the Zscaler/CASB proxy, and capture proxy packet logs.
3. **Preserve Immutable AI Inference Logs (`EU AI Act Art. 26(6)`):**
   * Lock input payloads, model version headers, confidence scores, and override timestamps in S3 Object-Lock storage (`7-year` financial archive) for CBI and vendor forensic inspection.

---

## 4. The Regulatory, Vendor & Client Clock (`T+45 Mins to T+30 Days`)

Log every filing and vendor notice across [`pillar-03-dora-incident-cbi-clock.xlsx`](../pillar-03-dora-incident-cbi-clock.xlsx) and [`pillar-06-eu-ai-act-inventory-and-fria.xlsx`](../../pillar-06-eu-ai-act-governance/pillar-06-eu-ai-act-inventory-and-fria.xlsx):

* **`T + 45 Minutes` (Hard Gate — DORA & EU AI Act Triage):**
  * Head of ICT Risk determines whether the AI failure constitutes a **DORA Major Incident** (`RTS 2024/1772`) and/or an **EU AI Act `Article 26(5)` / `Article 73` Serious Incident**.
* **`<= 4 Hours` (CBI Portal Initial Notification & Vendor Notice):**
  * Submit the **DORA Article 19(4)(a) Initial Notification** on the CBI Portal (if `CIBS` thresholds were breached) and issue a formal **`EU AI Act Article 26(5)` Suspension & Serious Risk Notice** to the third-party AI vendor.
* **`<= 72 Hours` (CBI Intermediate Report & DPC GDPR Filing):**
  * Submit the **DORA Intermediate Report** (`72h`) to the CBI Portal.
  * If customer `PII` or biometric data was exposed via prompt injection or unredacted LLM egress, the DPO submits a **GDPR Article 33 breach notification** to the **Irish Data Protection Commission (DPC)** within `72 hours`.
* **`<= 72 Hours` (Affected Customer Remediation — `DORA Art. 19(3)`):**
  * Re-process any transactions or onboarding applications wrongly blocked/declined during the malfunction window and notify affected customers transparently.
* **`<= 30 Calendar Days` (Final CBI Report, Vendor Audit & FRIA Update):**
  * Submit the final Root Cause Analysis (`RCA`) to the CBI Portal (`DORA Art. 19(4)(c)`), require an updated **bias/conformity audit pack** from the vendor before re-enabling the API, and update the system's **`Article 27` FRIA** in Pillar 6.

---

## 5. Re-Enablement Hard Gate (Post-Malfunction)

**No suspended third-party AI API may be re-enabled in production solely on the vendor's verbal assurance.** Before toggling the feature flag back on:
1. The vendor must provide a written **Root Cause & Model Patch Attestation** confirming the defect or bias drift is resolved.
2. Engineering and 2nd Line Risk must run a **shadow-mode replay** (scoring live traffic asynchronously without blocking customers) for at least `48 hours` to verify false-positive/reject rates sit safely within Pillar 6 thresholds.
3. `PCF-52` (or `CRO`) and Head of ICT Risk must co-sign re-activation in [`pillar-06-vendor-ai-assurance-and-llm-dlp.xlsx`](../../pillar-06-vendor-ai-assurance-and-llm-dlp.xlsx).
