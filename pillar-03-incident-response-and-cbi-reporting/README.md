---
title: Pillar 3 — Incident Detection, Classification & CBI 4-Hour Reporting Clock
---

# Pillar 3: Incident Detection, Classification & CBI Reporting
**Regulatory Basis:** DORA Chapter III (Articles 17–23) · EU Delegated Regulation 2024/1772 (Major Incident Classification) · EU Implementing Regulation 2025/302 (Reporting Templates) · Central Bank of Ireland (CBI) Cross-Industry Guidance on Operational Resilience (*Respond & Recover*, Guidelines 11–13)

---

## 1. What Pillar 3 Means in Practice
When a payment rail degrades or a security alert fires at 2:00 AM, engineers focus on restoring service—while the **Central Bank of Ireland (CBI)** enforces strict statutory clocks for incident classification, regulatory notification, and customer communication.

Pillar 3 removes ambiguity during live incidents by enforcing three operational rules:
1. **Separate Awareness vs. Classification Timestamps:** Under DORA, the **4-hour statutory clock** for submitting an Initial Notification via the **CBI Portal** starts at the exact minute the incident is *classified as Major* (with a hard outer ceiling of 24 hours from initial awareness). Internal triage must complete within **45 minutes** of detection.
2. **Deterministic EU RTS 2024/1772 Threshold Triage:** Instead of subjective severity calls, incidents affecting `CIBS-01` to `CIBS-05` are scored against the six EU RTS materiality criteria. Either *malicious unauthorised access risking data loss* (`Art. 9(5)(b)`) OR breaching **two or more** quantitative thresholds classifies the event as **Major**.
3. **Closed-Loop Recurring Incident & CAPA Review:** Minor incidents sharing a root cause within 6 months are aggregated monthly (`Art. 8(2)`), and every Major incident generates tracked Corrective & Preventive Actions (CAPAs) that feed back into Pillar 1 Impact Tolerances and Pillar 2 engineering controls.

---

## 2. Regulatory Alignment Matrix (DORA & CBI Requirements)

| Regulatory Anchor | Specific Supervisory Requirement | How Pillar 3 Operationalises It |
| :--- | :--- | :--- |
| **DORA Art. 17–18** & **Delegated Reg. 2024/1772 (Art. 1–9)** | Classify ICT-related incidents using uniform materiality thresholds (clients affected, transaction value, downtime, cross-border EEA impact, economic cost, data/reputational loss). | **`DORA_RTS_Triage_Engine`:** Evaluates all six criteria automatically and outputs `MAJOR - CBI REPORTABLE` vs. `NON-MAJOR - INTERNAL`. |
| **DORA Art. 19(1) & 19(4)** & **Implementing Reg. 2025/302** | Submit Initial Notification (`<= 4h` from classification / `<= 24h` from awareness), Intermediate Report (`<= 72h`), and Final RCA Report (`<= 1 month`) to the CBI Portal. | **`DORA_RTS_Triage_Engine`:** Auto-calculates exact statutory timestamps (`+4h`, `+72h`, `+30d`) the moment classification occurs. |
| **DORA Delegated Reg. 2024/1772 Art. 8(2)** | Aggregate recurring non-major incidents with the same root cause over a 6-month rolling window and escalate if cumulative thresholds are met. | **`Recurring_Incident_Review`:** Monthly review log flagging repeat incident clusters whose cumulative downtime (`>= 120m`) or cost (`>= €100k`) triggers Major status. |
| **DORA Art. 19(3)** & **CBI OpRes Guideline 11** | Notify clients without undue delay when an incident impacts their financial interests, and execute coordinated crisis communications. | **`Stakeholder_And_Client_Comms`:** Tracks client notices, GDPR 72h DPC notifications, and scheme/depositary bank escalations. |
| **DORA Art. 20** & **CBI OpRes Guideline 13** | Conduct formal post-incident root cause analysis (RCA) and remediate control gaps so lessons learned update resilience tolerances. | **`Post_Incident_CAPA_Log`:** Tracks root-cause fixes and links each action back to Pillar 1 (`CIBS` / `Risk Exceptions`) and Pillar 2 controls. |

---

## 3. End-to-End "2 AM" Incident Response & CBI Clock Process

1. **Step 1 — Detection & Technical Triage (`T+0` to `T+30 mins`):**
   * Automated SIEM, APM, or synthetic payment probes trigger an alert; on-call engineering logs the exact **Awareness Timestamp** and begins containment.
2. **Step 2 — Quantitative DORA RTS Classification (`<= T+45 mins`):**
   * The Incident Commander and 2nd Line ICT Risk Duty Officer enter impact metrics into **`DORA_RTS_Triage_Engine`**.
   * **Hard Gate:** Classification must be recorded within **45 minutes** of awareness. If malicious unauthorised access is confirmed OR `>= 2` quantitative thresholds are breached (`>= 10%` clients/daily value, `>= 120 mins` CIBS downtime, `>= 2` EEA Member States, `>= €100k` cost, or data/reputational breach), the incident is locked as **Major** and the 4-hour CBI clock starts immediately.
3. **Step 3 — War Room, CBI Initial Notice (`<= +4h`) & Client Comms:**
   * **< 2 Hours:** Issue client notification via status page / in-app banner if client financial interests or payment execution are impacted (`DORA Art. 19(3)`), logged in **`Stakeholder_And_Client_Comms`**.
   * **< 4 Hours:** Head of ICT & InfoSec Risk submits the **Initial Notification** via the **Central Bank of Ireland Portal** (`Implementing Reg. 2025/302`) with CEO (`PCF-1`) / PCF-56 sign-off.
   * **< 72 Hours:** Submit **Intermediate Report** to CBI Portal (and **DPC** notification if personal data breach is confirmed under GDPR Art. 33).
4. **Step 4 — Final RCA (`<= 30 Days`) & Closed-Loop CAPA:**
   * Within **30 calendar days** of classification, submit the **Final Root Cause Analysis Report** to the CBI Portal and log all corrective actions in **`Post_Incident_CAPA_Log`**.

---

## 4. "2 AM" Crisis RACI & Accountability Matrix

| Incident & Reporting Activity | On-Call Tech Lead (1st Line) | Incident Commander (Ops / CTO) | Head of ICT & InfoSec Risk (2nd Line) | CEO (PCF-1) / Safeguarding (PCF-56) | Legal / DPO / Compliance |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Technical Containment & Service Restoration** | **R** | **A** | **I** | **I** | **I** |
| **45-Min DORA RTS Severity Classification** | **C** | **R** | **A** | **I** | **C** |
| **Client Financial Impact Notice (`Art. 19(3)`)** | **I** | **C** | **C** | **A** | **R** |
| **CBI Portal Initial (`4h`), Intermediate (`72h`) & RCA (`30d`)** | **C** | **C** | **R** | **A (Sign-Off)** | **C** |
| **GDPR 72h DPC & Card Scheme / Bank Notices** | **I** | **I** | **C** | **A** | **R** |
| **Post-Incident CAPA Closure & Pillar 1/2 Update** | **R** | **R** | **A / Verify** | **I** | **I** |

*(**R** = Responsible, **A** = Accountable, **C** = Consulted, **I** = Informed)*

---

## 5. Target Incident & Reporting KPIs

| Metric / Outcome | Target Benchmark | How It Is Measured |
| :--- | :--- | :--- |
| **Mean Time to Classify (MTTC)** | `100%` of incidents classified within `45 minutes` | `MTTC (Mins)` column in `DORA_RTS_Triage_Engine` |
| **CBI Statutory Reporting Timeliness** | `100%` of `4h`, `72h`, and `30d` CBI Portal filings on time | Calculated statutory timestamps in `DORA_RTS_Triage_Engine` |
| **Client & DPC Notification Compliance** | `100%` of `Art. 19(3)` client notices & `72h` DPC filings met | `Comms Compliance Verdict` in `Stakeholder_And_Client_Comms` |
| **Recurring Minor Incident Review** | `100%` monthly Art. 8(2) cluster aggregation completed | `Recurring_Incident_Review` escalation status |
| **Post-Incident CAPA Closure** | `100%` of Major incident CAPAs closed within `30 days` | `Remediation Status` in `Post_Incident_CAPA_Log` |

---

## 6. Supporting Excel Registers
All live incident classifications, statutory CBI deadlines, crisis communication logs, and post-incident CAPAs are maintained across two companion Excel workbooks in this folder:

1. **[`pillar-03-dora-incident-cbi-clock.xlsx`](pillar-03-dora-incident-cbi-clock.xlsx)**
   * **`Incident_Command_Dashboard`:** KPI summary cards and MTTC vs. 45-minute SLA chart.
   * **`DORA_RTS_Triage_Engine`:** Automated EU Delegated Reg. 2024/1772 threshold evaluator and `+4h / +72h / +30d` CBI deadline calculator.
   * **`Recurring_Incident_Review`:** 6-month rolling aggregation tracker for recurring minor incidents (`Art. 8(2)`).
2. **[`pillar-03-crisis-comms-and-capa-log.xlsx`](pillar-03-crisis-comms-and-capa-log.xlsx)**
   * **`Comms_And_CAPA_Dashboard`:** Notification compliance KPIs and CAPA remediation chart.
   * **`Stakeholder_And_Client_Comms`:** Audit log for DORA Art. 19(3) client notices, GDPR 72h DPC filings, and scheme/bank escalations.
   * **`Post_Incident_CAPA_Log`:** Root-cause action register feeding lessons learned back into Pillars 1 and 2.
