---
title: Pillar 2 — ICT Protection, Asset Management & Change Control
---

# Pillar 2: ICT Protection, Asset Management & Change Control
**Regulatory Basis:** DORA Chapter II (Articles 8–9 & DORA RTS on ICT Risk Management) · Central Bank of Ireland (CBI) Operational Resilience Guidance (*Identify & Prepare*, Guideline 5) · CBI IT & Cybersecurity Risk Guidance · PCI-DSS v4.0 · EU AI Act Article 15

---

## 1. What Pillar 2 Means in Practice
Once Pillar 1 establishes *which* external business services (`CIBS-01` to `CIBS-05`) are critical to the Payment Institution and how long they can tolerate disruption, **Pillar 2 protects the underlying technology stack that keeps those payment rails running**.

In a Central Bank of Ireland–regulated Payment Institution, Pillar 2 answers two operational questions that supervisory inspectors and external auditors test first:
1. **Structural Containment (Architecture & Scope):** Do we maintain an accurate inventory of every system, cryptographic key, and privileged admin account supporting our payment and safeguarding rails—and have we isolated raw cardholder data inside a minimal **PCI-DSS v4.0 Cardholder Data Environment (CDE)**?
2. **Operational Hygiene (Patching & Change Control):** Do we remediate critical vulnerabilities within strict risk-based SLAs, and do we prevent untested code releases or unvetted AI integrations from causing production outages or customer data leaks?

---

## 2. Regulatory Alignment Matrix (DORA, CBI & Payment Standards)

| Regulatory Anchor | Specific Supervisory Requirement | How Pillar 2 Operationalises It |
| :--- | :--- | :--- |
| **DORA Art. 8 (Identification)** & **DORA RTS Art. 4–5** | Identify, classify, and document all ICT assets, configurations, and information assets supporting critical functions. | **`ICT_Asset_Inventory`:** Maps every microservice, database, HSM, and AI endpoint directly to its supported `CIBS` ID and 1st Line owner. |
| **CBI Operational Resilience Guidance — Pillar 1 (*Identify & Prepare*, Guideline 5)** | Map the exact technology and infrastructure dependencies required to deliver Critical or Important Business Services. | **`ICT_Asset_Inventory`:** Proves end-to-end traceability from external payment rails down to AWS/GCP regions and Equinix enclaves. |
| **DORA Art. 9 (Protection & Prevention)** & **DORA RTS Art. 6–7, 13–14** | Enforce network segmentation, encryption at rest/in transit, and cryptographic key lifecycle rotation. | **`Crypto_And_Key_Lifecycle`:** Tracks AES-256 / TLS 1.3 enforcement, FIPS 140-3 HSM key rotation schedules, and **PCI-DSS v4.0** CDE isolation. |
| **DORA RTS Art. 20–21** & **CBI IT/Cybersecurity Risk Guidance (*Access Management*)** | Restrict privileged access using MFA, Just-In-Time (JIT) elevation, and periodic recertification. | **`Privileged_Access_Review`:** Enforces 90-day access reviews for HSM key custodians, Core Ledger DBAs, and Safeguarding Bank portal approvers. |
| **DORA Art. 9(2)** & **DORA RTS Art. 8–10** | Operate automated vulnerability scanning and enforce risk-based patch remediation timelines. | **`Vuln_Remediation_Tracker`:** Auto-calculates `7-day` Critical / CISA KEV and `30-day` High patch deadlines with automated SLA breach alerts. |
| **DORA RTS Art. 16–17**, **CBI Change Management Guidance**, & **EU AI Act Art. 15** | Govern ICT changes so poorly tested deployments or AI data flows do not compromise availability or data integrity. | **`CICD_Change_Gates`:** Enforces pre-release gates requiring SAST scans, rollback verification, PCI CDE checks, and AI egress DLP validation. |

---

## 3. End-to-End Operating Process & Hard Decision Gates

1. **Step 1 — Asset Tagging & PCI-DSS v4.0 CDE Containment:**
   * Every new microservice, database, or AI endpoint must be tagged in the CMDB with its supported `CIBS` ID, data classification, and PCI-DSS scope (`In-Scope (CDE)`, `Connected-to-CDE`, or `Out-of-Scope (Tokenized)`) inside **`ICT_Asset_Inventory`**.
   * **Hard Gate:** Any proposed service handling raw card PANs outside the isolated PCI Tokenization Vault (`AST-003`) is blocked at architecture review.
2. **Step 2 — Cryptographic Key & Quarterly Privileged Access Control:**
   * Encryption keys and signing certificates are logged in **`Crypto_And_Key_Lifecycle`** with automated 30-day renewal alerts.
   * High-privilege roles across AWS, Cloud HSM, Core Ledger, and Safeguarding Bank portals undergo mandatory 90-day recertification in **`Privileged_Access_Review`**.
3. **Step 3 — Risk-Based Vulnerability Triage & Patch SLAs:**
   * Weekly vulnerability scan findings are triaged in **`Vuln_Remediation_Tracker`** using CVSS severity and CISA Known Exploited Vulnerability (KEV) status:
     * **Critical (`CVSS >= 9.0`) or CISA KEV:** `7 calendar days`
     * **High (`CVSS 7.0–8.9`):** `30 calendar days`
     * **Medium (`CVSS 4.0–6.9`):** `90 calendar days`
   * **Hard Gate:** Any Critical/KEV finding that cannot be patched within 7 days requires an immediate virtual patch/compensating control and a formal time-bound exception logged in Pillar 1 (`Risk_Exception_Register`).
4. **Step 4 — CI/CD Pre-Release Change Gate:**
   * Before deploying changes to production payment or safeguarding services, engineering logs release checks in **`CICD_Change_Gates`**.
   * **Hard Gate:** Production deployment is blocked unless SAST/secret scans pass, a rollback plan is tested, AI egress DLP rules are verified (for AI-enabled services), and 2nd Line ICT Risk approves high-impact releases.

---

## 4. RACI & Accountability Matrix

| Protection & Change Activity | CTO / 1st Line Engineering | Security Architecture / SecOps | Head of ICT & InfoSec Risk (2nd Line) | Head of Safeguarding (PCF-56) |
| :--- | :---: | :---: | :---: | :---: |
| **Production Asset Tagging & CMDB Accuracy** | **R / A** | **C** | **I / Assurance** | **I** |
| **PCI-DSS v4.0 CDE Boundary & HSM Key Management** | **R** | **R** | **A / Challenge** | **I** |
| **Quarterly Privileged Access Recertification (PAM)** | **R** | **C** | **A** | **A (Bank Portals)** |
| **Vulnerability Patching Within 7d / 30d SLAs** | **R / A** | **C** | **I / Escalation** | **I** |
| **CI/CD Change Gate Sign-Off (High-Impact / CDE / AI)** | **R** | **C** | **A** | **C (Ledger Changes)** |

*(**R** = Responsible, **A** = Accountable, **C** = Consulted, **I** = Informed)*

---

## 5. Target Hygiene Outcomes & KPIs

| Metric / Outcome | Target Benchmark | How It Is Measured |
| :--- | :--- | :--- |
| **Critical / CISA KEV Patch SLA** | `>= 95%` remediated within `7 calendar days` | `SLA Verdict` formula in `Vuln_Remediation_Tracker` |
| **PCI-DSS v4.0 CDE Scope Containment** | `<= 25%` of production assets in CDE scope | `Asset_And_CDE_Dashboard` scope breakdown |
| **Cryptographic Key Hygiene** | `0` overdue master keys or ISO 20022 signing certs | `Lifecycle Status` in `Crypto_And_Key_Lifecycle` |
| **Quarterly PAM Recertification** | `100%` of privileged roles reviewed within `90 days` | `Review Status` in `Privileged_Access_Review` |
| **Production Change Gate Integrity** | `0` high-risk changes deployed without rollback & DLP checks | `Gate Verdict` formula in `CICD_Change_Gates` |

---

## 6. Supporting Excel Registers
All live asset inventories, cryptographic schedules, PAM reviews, vulnerability SLAs, and release change gates are maintained across two companion Excel workbooks in this folder:

1. **[`pillar-02-asset-crypto-and-pam-scope.xlsx`](pillar-02-asset-crypto-and-pam-scope.xlsx)**
   * **`Asset_And_CDE_Dashboard`:** KPI summary cards and PCI-DSS v4.0 CDE scope chart.
   * **`ICT_Asset_Inventory`:** Master mapping of production services to `CIBS` IDs, hosting regions, and CDE boundaries.
   * **`Crypto_And_Key_Lifecycle`:** Encryption standards and automated rotation tracking for HSM/KMS keys and certificates.
   * **`Privileged_Access_Review`:** 90-day recertification tracker for HSM custodians, DBAs, and safeguarding portal approvers.
2. **[`pillar-02-vuln-and-change-gate-tracker.xlsx`](pillar-02-vuln-and-change-gate-tracker.xlsx)**
   * **`Hygiene_And_Change_Dashboard`:** Vulnerability SLA posture chart and release gate KPIs.
   * **`Vuln_Remediation_Tracker`:** Automated CVSS/KEV SLA due-date calculator and breach detector.
   * **`CICD_Change_Gates`:** Pre-release security, rollback, and AI egress DLP verification log.
