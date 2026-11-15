---
title: Pillar 3 — Incident Response, Playbooks & The CBI 4-Hour Reporting Clock
---

# Pillar 3: Incident Response, Playbooks & The CBI 4-Hour Reporting Clock
**Regulatory Basis:** DORA Chapter III (Articles 17–23) · DORA RTS on Major Incident Classification (Delegated Regulation (EU) 2024/1772) · DORA ITS on Incident Reporting Templates (Implementing Regulation (EU) 2025/302) · Central Bank of Ireland (`CBI`) Operational Resilience Guidance (Guidelines 11–13) · GDPR Articles 33–34

---

## 1. Why Pillar 3 Works This Way (Plain-English Q&A)

### Why do you enforce a strict 45-minute triage clock when DORA gives 4 hours to notify the CBI?
**Because waiting 3 hours to decide if an incident is "Major" guarantees a late regulatory filing.**
Under **DORA Article 19(4)(a)**, once an ICT-related incident is classified as **Major**, the Payment Institution has just **4 hours** to submit its Initial Notification on the Central Bank of Ireland (`CBI`) Portal (and no more than `24 hours` from initial detection). If engineering and compliance spend three hours debating severity, there is zero time left to draft, review, and file an accurate notice. Our **45-minute classification hard gate** forces an early, deterministic decision.

### Why separate technical recovery from regulatory command during an outage?
**Because engineers debugging a live database failover cannot simultaneously calculate EU RTS thresholds or write client notices.**
During any severe disruption, we split into two parallel tracks within 15 minutes: **1st Line Engineering** focuses 100% on technical containment and failover, while **2nd Line ICT Risk & Compliance (`PCF-52`)** run the DORA reporting clock, activate out-of-band communication channels, and enforce anti-fraud guardrails across operations.

### What if an incident is minor—do you just close the ticket and move on?
**No—recurring minor incidents must be aggregated monthly under DORA RTS `Article 8(2)`.**
A series of small 10-minute payment timeouts that individually fall below Major thresholds can collectively indicate a systemic flaw. Every minor incident is logged in [`pillar-03-crisis-comms-and-capa-log.xlsx`](pillar-03-crisis-comms-and-capa-log.xlsx) (`Minor_Incident_Aggregation`) and reviewed monthly to catch recurring patterns before they cause a major outage.

---

## 2. End-to-End Operating Process & Hard Decision Gates

1. **Step 1 — Detection, Containment & Scenario Playbook Activation (`T+0 to T+15 Mins`):**
   * Alerts from APM/SIEM, MDR, or third-party vendor status pages trigger immediate containment and activate the matching scenario playbook in [`playbooks/`](playbooks/):
     * [`irp-01-core-payment-rail-outage.md`](playbooks/irp-01-core-payment-rail-outage.md) (SEPA Instant / Card Acquiring / AWS AZ failure)
     * [`irp-02-ransomware-and-data-extortion.md`](playbooks/irp-02-ransomware-and-data-extortion.md) (Active intrusion, ransomware & out-of-band containment)
     * [`irp-03-enterprise-m365-outlook-outage.md`](playbooks/irp-03-enterprise-m365-outlook-outage.md) (Enterprise Exchange Online outage, anti-BEC freeze & portal fallback)
     * [`irp-04-third-party-ai-malfunction.md`](playbooks/irp-04-third-party-ai-malfunction.md) (EU AI Act `Art. 26(5)`/`73` API kill-switch & GenAI DLP breach)
   * **HARD GATE 1 (Out-of-Band & Anti-Fraud Gate):** If corporate email/M365 (`IRP-03`) or domain identity (`IRP-02`) is affected, command immediately moves to Signal/Slack out-of-band bridges and an all-staff freeze is issued prohibiting personal email or consumer messaging workarounds.
2. **Step 2 — Deterministic `DORA RTS 2024/1772` Threshold Triage (`T+15 to T+45 Mins`):**
   * Head of ICT Risk scores the incident in [`pillar-03-dora-incident-cbi-clock.xlsx`](pillar-03-dora-incident-cbi-clock.xlsx) (`DORA_RTS_Threshold_Triage`) across all EU RTS criteria: malicious unauthorized access, clients/transactions affected, EUR value impacted, `CIBS` duration vs. Board `RTO`, geographical spread, and data loss.
   * **HARD GATE 2 (45-Minute Classification Deadline):** Classification (`MAJOR` vs. `MINOR`) must be locked within **45 minutes** of detection. Any confirmed malicious intrusion touching `CIBS` infrastructure is presumed `MAJOR` automatically.
3. **Step 3 — Statutory Filings (`4h` / `72h`) & Client Notifications (`DORA Art. 19(3)`):**
   * For `MAJOR` incidents, `PCF-52` (Head of Compliance/MLRO) and Head of ICT Risk execute timestamped filings in `CBI_4h_72h_30d_Tracker`:
     * **`<= 4 Hours` from Classification:** Initial Notification on **CBI Portal** + client/merchant advisory (`Client_Art19_Comms_Log`).
     * **`<= 72 Hours` from Initial Notice:** Intermediate Report on **CBI Portal** (plus **GDPR `Art. 33` DPC filing** within `72h` if personal data is breached).
   * **HARD GATE 3 (Dual-Sign-Off Regulatory Filing Gate):** No CBI Portal or DPC filing may be submitted without joint review by Head of ICT Risk (technical accuracy) and `PCF-52` (regulatory completeness).
4. **Step 4 — 30-Day Root Cause Analysis (`RCA`), `CAPA` Closure & Minor Aggregation (`T+Recovery to T+30d`):**
   * Within **30 calendar days**, the Final Report (`DORA Art. 19(4)(c)`) is filed on the CBI Portal, and permanent corrective actions (`CAPAs`) are tracked to verified closure in [`pillar-03-crisis-comms-and-capa-log.xlsx`](pillar-03-crisis-comms-and-capa-log.xlsx) (`RCA_And_CAPA_Closure_Log`).
   * **HARD GATE 4 (30-Day `CAPA` Closure Gate):** Any `CAPA` remaining open past `30 days` automatically flags `OVERDUE - ESCALATE` for the monthly Operational Risk & Resilience Committee (`ORRC`) and feeds directly into Pillar 4's next resilience test cycle.

---

## 3. RACI & Accountability Matrix

| Pillar 3 Incident & Reporting Activity | CEO (`PCF-1`) & CRO (`PCF-14`) | Head of Compliance / MLRO (`PCF-52`) | CTO (`PCF-46`) & SRE / SecOps | DPO | Head of ICT & InfoSec Risk (2nd Line) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Technical Containment, Failover & Kill-Switches** | **I** | **I** | **R / A** | **I** | **C** |
| **45-Minute `DORA RTS 2024/1772` Classification Triage** | **I** | **C** | **C (Impact Data)** | **C** | **R / A** |
| **CBI Portal Filings (`4h` Initial / `72h` Interm. / `30d` Final)** | **A (Major Escalation)** | **R / A (Submitter)** | **C** | **C** | **R (Technical Lead)** |
| **GDPR `Art. 33` DPC Breach Notification (`<= 72h`)** | **I** | **C** | **C** | **R / A** | **C** |
| **Client & Merchant Notifications (`DORA Art. 19(3)`)** | **A** | **C (Legal Review)** | **I** | **C** | **R** |
| **30-Day `RCA`, `CAPA` Closure & Monthly `Art. 8(2)` Rollup** | **I** | **C** | **R (Fix Execution)** | **I** | **A (Verification)** |

*(**R** = Responsible, **A** = Accountable, **C** = Consulted, **I** = Informed)*

---

## 4. Target Pillar 3 KPIs

| Metric / Outcome | Target Benchmark | Workbook & Formula Verification |
| :--- | :--- | :--- |
| **Mean Time to Classify (`MTTC`)** | `<= 45 minutes` from initial detection (`100%` within gate) | `Triage Minutes` in `DORA_RTS_Threshold_Triage` |
| **On-Time CBI Portal Regulatory Filings** | `100.0%` on-time `4-hour`, `72-hour`, and `30-day` submissions | `Filing SLA Status` in `CBI_4h_72h_30d_Tracker` |
| **30-Day `RCA` & `CAPA` Closure Rate** | `100.0%` of post-incident `CAPAs` verified closed within `30 days` | `CAPA Status` in `RCA_And_CAPA_Closure_Log` |
| **Monthly Minor Incident Aggregation (`Art. 8(2)`)** | `100.0%` monthly review of recurring minor incidents | `Minor_Incident_Aggregation` tab |

---

## 5. Scenario Playbooks & Supporting Excel Registers

### Scenario-Specific Incident Response Playbooks (`playbooks/`)
1. **[`playbooks/irp-01-core-payment-rail-outage.md`](playbooks/irp-01-core-payment-rail-outage.md)** — SEPA Instant / Card Acquiring / AWS Availability Zone outage (`30-min` RTO protection & `RPO = 0` queue reconciliation).
2. **[`playbooks/irp-02-ransomware-and-data-extortion.md`](playbooks/irp-02-ransomware-and-data-extortion.md)** — Destructive intrusion, volatile memory preservation, out-of-band Signal command, and dual CBI/DPC clocks.
3. **[`playbooks/irp-03-enterprise-m365-outlook-outage.md`](playbooks/irp-03-enterprise-m365-outlook-outage.md)** — Third-party Exchange Online/Entra ID disruption, mandatory anti-BEC/Shadow-IT freeze, and Client Portal payment fallback.
4. **[`playbooks/irp-04-third-party-ai-malfunction.md`](playbooks/irp-04-third-party-ai-malfunction.md)** — EU AI Act `Art. 26(5)`/`73` `60-second` API kill-switch, rules fallback, and GenAI egress DLP containment.

### Companion Excel Registers
1. **[`pillar-03-dora-incident-cbi-clock.xlsx`](pillar-03-dora-incident-cbi-clock.xlsx)** — `Incident_Clock_Dashboard` · `DORA_RTS_Threshold_Triage` · `CBI_4h_72h_30d_Tracker`
2. **[`pillar-03-crisis-comms-and-capa-log.xlsx`](pillar-03-crisis-comms-and-capa-log.xlsx)** — `Crisis_CAPA_Dashboard` · `Client_Art19_Comms_Log` · `RCA_And_CAPA_Closure_Log` · `Minor_Incident_Aggregation`
