---
title: Quarterly Board ICT & AI Risk Report + KRI Dashboard
---

# Board Risk Committee Pack: ICT, Operational Resilience & AI Risk Report
**Entity Profile:** Irish-Authorised Payment Institution (PI/EMI)  
**Prepared By:** Head of ICT & InfoSec Risk (2nd Line of Defence)  
**Submitted To:** Board Risk Committee (BRC) & Executive Management Committee  
**Regulatory Basis:** DORA Article 5 (Management Body Governance), CBI Cross-Industry Operational Resilience Guidance, CBI Individual Accountability Framework (IAF / PCF Governance), & EU AI Act  

---

## 1. Executive Summary & Overall Risk Posture
* **Overall ICT & InfoSec Risk Rating:** **AMBER (Stable — Within Board Risk Appetite)**
* **Key Quarter Highlights:**
  * **Operational Resilience:** Zero DORA-reportable major ICT incidents across SEPA Instant and card acquiring rails (`99.98%` core ledger availability). Annual **CBI Operational Resilience Self-Assessment** and **ICT Self-Assessment Tool (ICT-SAT)** completed and submitted on schedule.
  * **Safeguarding & Payments Integrity:** `100%` adherence to `D+1` safeguarding sweeps and daily ISO 20022 external reconciliations with zero unapproved discrepancies.
  * **AI Governance:** All 5 production AI/ML systems mapped in the **EU AI Act Inventory**; Article 50 customer chatbot transparency disclosures live; zero unapproved external LLM endpoints detected via cloud egress monitoring.
  * **Key Watch Item (Amber):** Critical vulnerability remediation SLA dipped to `91%` (target `>= 95%`) due to a third-party card-vault maintenance window deferral; formal compensating controls and a 14-day remediation commitment are tracked below.

---

## 2. Three Lines of Defence & CBI PCF Accountability Mapping
In alignment with **DORA Article 5** and the **Central Bank of Ireland (CBI) Individual Accountability Framework (IAF)**, ICT and operational resilience responsibilities are explicitly delineated across Pre-Approval Controlled Functions (PCFs) and 2nd Line oversight:

| Governance Role / Function | CBI PCF / Line | Core ICT, Resilience & AI Accountability |
| :--- | :--- | :--- |
| **Board Risk Committee (INED Chair)** | **PCF-3 / PCF-5** *(Board Oversight)* | Approves ICT Risk Management Framework, risk appetite thresholds, annual Operational Resilience Self-Assessment, and **TIBER-IE** testing scope; completes mandatory annual DORA & AI governance training. |
| **Chief Executive Officer** | **PCF-1 / PCF-8** *(1st Line Executive)* | Ultimate executive accountability for firm-wide operational resilience, safeguarding governance, and **PSD3 / PSR** re-authorisation readiness. |
| **Chief Technology Officer** | **1st Line Delivery** *(Tech & Engineering)* | Executes cloud security hardening, patching SLAs, CDE segmentation, disaster recovery failover tests, and technical AI/DLP guardrails. |
| **Head of ICT & InfoSec Risk** | **2nd Line Assurance** *(Independent Risk)* | Owns ICT/AI Risk Frameworks, **DORA Register of Information (RoI)** quality assurance, CBI major incident classification, vendor due diligence, and independent challenge of risk acceptances. |
| **Head of Safeguarding Oversight** | **PCF-56** *(Safeguarding Governance)* | Oversees daily safeguarding reconciliations (`SAF-01` to `SAF-05`), depositary bank concentration limits, and annual **ISAE 3000** assurance audit. |
| **MLRO / Head of Financial Crime** | **PCF-52** *(Financial Crime & Fraud)* | Owns real-time fraud/AML scoring thresholds, human-in-the-loop override SLAs (`AI-001`), and biometric eKYC compliance (`AI-004`). |

---

## 3. Quarterly Key Risk Indicator (KRI) Dashboard

| KRI ID | Risk Domain & Metric | Board Risk Appetite (Green) | Escalation Trigger (Red) | Current Quarter | Status | Management Action / Commentary |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **KRI-01** | **SEPA Instant & Core Ledger Availability** | `>= 99.95%` (`RTO < 2h`) | `< 99.90%` (`RTO > 4h`) | `99.98%` | **GREEN** | Bi-annual active-passive failover test (`eu-west-1` to `eu-central-1`) completed in `38 mins`. |
| **KRI-02** | **DORA Major Incident Classification SLA** | `100%` classified `< 2h` of detection | Any breach of 4h CBI initial clock | `100%` (`0` Major) | **GREEN** | 2 minor third-party webhook latency alerts triaged within `22 mins`; non-reportable under DORA thresholds. |
| **KRI-03** | **Critical Vulnerability Remediation (`CVSS >= 9.0`)** | `>= 95%` patched within `7 days` | `< 85%` or any exploit-active > `7d` | `91.0%` | **AMBER** | 1 vendor-managed HSM appliance patch deferred pending scheduled maintenance window; WAF virtual patch active. |
| **KRI-04** | **Safeguarding Reconciliation Variance (`> €0.01`)** | `0` unresolved breaks `> T+1` | Any unescalated break `> T+1` | `0` breaks | **GREEN** | `100%` automated daily `camt.053` matching verified ahead of annual ISAE 3000 fieldwork. |
| **KRI-05** | **DORA Critical ICT Vendor Exit Plan Testing** | `100%` CIF exit plans reviewed/tested annually | Overdue `> 30 days` | `100%` | **GREEN** | Tabletop exit simulation completed for Core Payment Ledger (`ICT-2026-001`); XBRL RoI dry-run clean. |
| **KRI-06** | **AI Fraud False-Positive Analyst Override SLA** | `>= 98%` reviewed `< 15 mins` | `< 90%` or unapproved AI API | `99.2%` | **GREEN** | Zero shadow AI egress alerts; Article 50 disclosure audit passed across web and mobile chat channels. |

---

## 4. Formal Risk Acceptance & Exception Register (2nd Line Governance)
Under the firm's ICT Risk Governance Charter, 1st Line Engineering cannot silently defer security controls. Any temporary exception requires a documented compensating control, an expiry date (`<= 90 days`), and formal sign-off by the **Head of ICT & InfoSec Risk** (or the **Board Risk Committee** for High residual risks):

| Exception ID | Control / Policy Gap | Business Justification | Compensating Controls | Residual Risk | Approver & Expiry |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **EXC-2026-04** | **KRI-03 Patch Deferral:** HSM management interface firmware update delayed by 12 days (`CVSS 9.1`). | Requires coordinated maintenance freeze with card scheme processor (`ICT-2026-003`). | Management interface isolated to jump-host bastion with hardware MFA; IPS virtual signature deployed; 24/7 SIEM alerting. | **Low-Medium** *(Post-mitigation)* | Approved by **Head of ICT Risk & CTO** — Expires in `12 days`. |
| **EXC-2026-05** | **Legacy Merchant API TLS 1.2 Support:** 2 enterprise merchants still migrating to TLS 1.3 / mTLS. | Prevents settlement disruption for €14M/month merchant volume during Q4 peak. | Restricted to strong AEAD cipher suites only; IP allow-listing enforced; contractual cutover mandate signed. | **Low
