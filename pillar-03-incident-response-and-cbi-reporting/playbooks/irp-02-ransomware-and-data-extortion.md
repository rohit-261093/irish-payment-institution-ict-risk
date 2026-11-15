---
title: IRP-02 — Ransomware, Destructive Intrusion & Data Extortion Playbook
---

# IRP-02: Ransomware, Destructive Intrusion & Data Extortion
**Playbook ID:** `IRP-02` · **Primary Pillar:** Pillar 3 (`pillar-03-incident-response-and-cbi-reporting/`) · **Linked Registers:** [`pillar-03-dora-incident-cbi-clock.xlsx`](../pillar-03-dora-incident-cbi-clock.xlsx) & [`pillar-03-crisis-comms-and-capa-log.xlsx`](../pillar-03-crisis-comms-and-capa-log.xlsx)

---

## 1. Trigger & Severity Classification (`T+0`)

### Activation Triggers
Activate `IRP-02` immediately upon any confirmed or high-confidence indicator of malicious encryption, unauthorized lateral movement, or bulk data staging/exfiltration:
* **EDR / MDR Critical Containment Alert:** CrowdShield 24/7 MDR or EDR detects mass file encryption, shadow-copy deletion (`vssadmin`), Cobalt Strike / C2 beaconing, or unauthorized privilege escalation (`PAM` bypass) on production or corporate endpoints.
* **CDE / Vault Anomaly (`CIBS-02`):** Unauthorized access attempt against the PCI Tokenization Vault, FIPS 140-3 Cloud HSM cluster, or core PostgreSQL database (`CIBS-01`, `CIBS-03`).
* **Extortion Demand / Dark-Web Leak:** Receipt of a ransom note, threat-actor extortion email, or threat-intelligence alert (`FS-ISAC` / `NCSC-IE`) confirming Payment Institution data on a leak site.

### Statutory & Regulatory Presumption
* **Automatic Major Incident Presumption (`DORA Art. 18` & `RTS 2024/1772`):** Any confirmed malicious intrusion affecting network/information systems supporting `CIBS-01`–`CIBS-05` or compromising confidential client/payment data meets the **Malicious & Unauthorised Access** criterion and is classified **Major** by default.
* **Dual Regulatory Clocks:** Triggers both the **DORA 4-hour Central Bank of Ireland (CBI) Portal notification clock** AND the **GDPR Article 33 72-hour Data Protection Commission (DPC) notification clock** (if personal data confidentiality/availability is impacted).

---

## 2. Out-of-Band Command & Roles (`T+0 to T+15 Mins`)

| Crisis Role | Designated Owner | Primary Responsibility During `IRP-02` |
| :--- | :--- | :--- |
| **Crisis Commander** | Head of ICT & InfoSec Risk / CISO | Directs containment strategy, network isolation, external DFIR retainer activation, and regulatory triage. |
| **Technical Containment Lead** | SecOps Lead & Principal SRE | Executes host isolation, IAM credential revocation, WAF/firewall blocks, and immutable backup verification. |
| **Executive Sponsor** | CEO (`PCF-1`) & CRO (`PCF-14`) | Chairs Executive Crisis Committee, approves emergency system shutdowns, and holds strict **no-ransom-payment** authority. |
| **Regulatory & Legal Lead** | Head of Compliance (`PCF-52`) & General Counsel | Manages CBI Portal (`4h`/`72h`/`30d`), DPC (`72h`), An Garda Síochána (`GNCCB`), and `NCSC-IE` notifications under legal privilege. |
| **Data Protection Officer** | DPO | Assesses PII/PAN exposure scope for GDPR `Art. 33` (DPC) and `Art. 34` (data subject) notices. |

* **Out-of-Band Command Rule:** **Assume corporate Microsoft 365, Slack, and internal VoIP may be monitored by the threat actor.** Conduct all incident command exclusively on the pre-provisioned **Signal Executive Crisis Group** and isolated out-of-band conference bridge.

---

## 3. Immediate Containment & Forensic Preservation (`T+15 to T+45 Mins`)

1. **Surgical Network & Identity Containment (Do Not Reboot Infected Hosts):**
   * **Preserve Volatile Memory:** Instruct SecOps and CrowdShield MDR to isolate compromised hosts via EDR network quarantine **without powering off or rebooting** (preserving RAM for forensic triage).
   * **Sever East-West Bridges:** Immediately close all non-essential VPC peering, bastion tunnels, and CI/CD deployment pipelines touching the PCI Tokenization Vault (`CIBS-02`) and Core Ledger (`CIBS-01`, `CIBS-03`).
   * **Global Identity Reset:** Revoke active OAuth/SSO refresh tokens in Entra ID, rotate emergency break-glass PAM credentials (`Pillar 2`), and enforce hardware FIDO2 re-authentication for all privileged administrators.
2. **Protect Immutable Backups & HSM Quorums:**
   * Verify S3 Object-Lock (`Compliance Mode`) backups and offline HSM key-quorum backups are air-gapped and untouched before initiating any restoration.
3. **Engage External Retainers:**
   * Activate the pre-contracted Digital Forensics & Incident Response (**DFIR**) retainer and external cyber breach counsel under legal professional privilege.

---

## 4. The Regulatory, Law Enforcement & Client Clock (`T+45 Mins to T+30 Days`)

Log every filing milestone in [`pillar-03-dora-incident-cbi-clock.xlsx`](../pillar-03-dora-incident-cbi-clock.xlsx):

* **`T + 45 Minutes` (DORA Classification & Executive Escalation):**
  * Confirm **Major ICT-Related Incident** status under `RTS 2024/1772` (malicious unauthorized access / critical service impact) and brief `PCF-1` (CEO) and `PCF-52` (MLRO).
* **`<= 4 Hours from Classification` (CBI Portal Initial Notification):**
  * Submit the **DORA Article 19(4)(a) Initial Notification** on the CBI Portal, noting active containment, forensic investigation status, and whether payment rails (`CIBS-01`/`CIBS-02`) remain isolated or operational.
* **`<= 24 Hours` (Law Enforcement & National CSIRT Engagement):**
  * File formal cybercrime report with **An Garda Síochána (Garda National Cyber Crime Bureau — GNCCB)** and share sanitized IoCs with **NCSC-IE** (`DORA Art. 19(2)` / `Art. 45`).
* **`<= 72 Hours` (CBI Intermediate Report & DPC GDPR Notification):**
  * Submit the **DORA Article 19(4)(b) Intermediate Report** to the CBI Portal.
  * If forensic triage confirms unauthorized access or exfiltration of customer PII/PANs, the DPO and `PCF-52` submit a **GDPR Article 33 breach notification** to the **Irish Data Protection Commission (DPC)** within `72 hours`.
* **`<= 72 Hours` (Client & Partner Notices — `DORA Art. 19(3)`):**
  * Issue factual, counsel-approved notifications to affected corporate merchants, depositary banks, and payment service users (without disclosing sensitive forensic vulnerabilities).
* **`<= 30 Calendar Days` (CBI Final Report & Root Cause Analysis):**
  * Submit the DFIR-verified Root Cause Analysis (`RCA`), initial access vector, confirmed data scope, and permanent `CAPA` roadmap under `DORA Article 19(4)(c)`.

---

## 5. Business Continuity & Extortion Governance Rules

1. **Strict Anti-Extortion Stance:** The Payment Institution maintains a strict policy against paying ransom demands without explicit Board, legal, and sanctions-screening (`OFAC`/`EU`) clearance; recovery relies exclusively on clean-room rebuilds from verified immutable backups.
2. **Clean-Room Rebuild Protocol:** No server or microservice in an affected subnet may be restored in place. All workloads must be redeployed from verified infrastructure-as-code (`Terraform`) templates into a clean AWS account/VPC, with fresh cryptographic keys generated via HSM ceremony (`Pillar 2`).

---

## 6. Recovery Verification & Post-Incident Closure (`T+Recovery to T+30 Days`)

1. **Forensic Clean-Bill-of-Health Gate:**
   * External DFIR leads and Head of ICT Risk must co-sign a written **Clean-Room Verification Certificate** (confirming zero persistence mechanisms, rotated secrets/keys, and patched initial access vector) before reconnecting any `CIBS` to live SEPA or card schemes.
2. **CAPA & TIBER-IE Integration:**
   * Record all structural security upgrades in [`pillar-03-crisis-comms-and-capa-log.xlsx`](../pillar-03-crisis-comms-and-capa-log.xlsx) (`RCA_And_CAPA_Closure_Log`).
   * Feed the threat actor's exact `MITRE ATT&CK` TTPs into **Pillar 4 (`TIBER_IE_And_Pentest_Findings`)** to validate detection and blocking rules via Purple-Team replay.
