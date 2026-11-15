---
title: Pillar 2 — ICT Protection, Cryptography, PAM & Change Control Gates
---

# Pillar 2: ICT Protection, Cryptography, PAM & Change Control Gates
**Regulatory Basis:** DORA Articles 8–9 · DORA RTS on ICT Risk Management Tools, Methods, Processes and Policies (Delegated Regulation (EU) 2024/1774) · Central Bank of Ireland (`CBI`) Cross-Industry Guidance on Information Technology and Cybersecurity Risks

---

## 1. Why Pillar 2 Works This Way (Plain-English Q&A)

### Why not patch every vulnerability strictly in order of CVSS score?
**Because CVSS scores measure theoretical severity, not exposure on our payment rails.**
A `CVSS 9.8` flaw on an isolated internal staging server poses far less immediate danger to Irish payment service users than an actively exploited `CVSS 7.8` flaw on an internet-facing SEPA Instant API gateway (`CIBS-01`). In [`pillar-02-vuln-and-change-gate-tracker.xlsx`](pillar-02-vuln-and-change-gate-tracker.xlsx), patch SLAs combine **CVSS severity**, **CISA Known Exploited Vulnerabilities (`KEV`)** status, and **`CIBS` criticality**.

### How do you prevent human error or rogue releases from taking down payment rails?
**By turning release checklists into automated CI/CD hard gates.**
In fast-moving fintech engineering, manual change advisory boards (`CABs`) either rubber-stamp everything or slow releases to a crawl. Instead, Pillar 2 automates low-risk standard changes while enforcing **hard pipeline gates** on high-risk changes touching `CIBS-01`–`CIBS-05`: no deployment can proceed without automated `SAST/SCA` security scans, verified rollback scripts, peer approval, and automated `PAN`/`PII` data-loss prevention (`DLP`) checks.

### Why are Cloud HSM keys and Privileged Access (`PAM`) tracked together?
**Because compromised admin credentials or expired cryptographic keys instantly bypass perimeter firewalls.**
Perimeter security means nothing if an engineer holds permanent root access or an unrotated Tokenization Key Encryption Key (`KEK`). Pillar 2 enforces Just-In-Time (`JIT`) privileged access with hardware `FIDO2` MFA and strict **90-day `PCF` access recertifications**.

---

## 2. End-to-End Operating Process & Hard Decision Gates

1. **Step 1 — Asset Discovery & `CIBS` Criticality Tagging (`Continuous / CMDB Sync`):**
   * Every cloud workload, database, API gateway, and HSM partition is inventoried in [`pillar-02-asset-crypto-and-pam-scope.xlsx`](pillar-02-asset-crypto-and-pam-scope.xlsx) (`ICT_Asset_CIBS_Inventory`) and tagged to its parent `CIBS` and encryption standard.
   * **HARD GATE 1 (Unclassified Asset Gate):** Any cloud resource deployed via Terraform/CI without mandatory `CIBS_ID`, `Data_Classification`, and `Owner` tags is blocked from receiving production network ingress.
2. **Step 2 — Cryptographic Key Lifecycle & Quarterly `PAM` Recertification (`90-Day Cycle`):**
   * Cryptographic keys (`AES-256-GCM`, `RSA-4096`, `TLS 1.3`) are tracked in `Cryptographic_Key_Lifecycle` with automated rotation alerts, while privileged entitlements (AWS Root, Cloud HSM Custodians, Depositary Bank Portals) undergo mandatory 90-day review in `PAM_Access_Recertification`.
   * **HARD GATE 2 (`PAM` Revocation Gate):** Any privileged entitlement not explicitly recertified by its `PCF` / system owner within `90 days` is automatically suspended in IAM/PAM (`REVOKED - OVERDUE`).
3. **Step 3 — Risk-Tiered Vulnerability & `CISA KEV` Remediation (`Daily Scans`):**
   * Container and infrastructure scanners feed `Vulnerability_SLA_Tracker`, enforcing hard SLAs: **`<= 7 days`** for Critical (`CVSS >= 9.0`) or `CISA KEV` flaws on `CIBS` assets, **`<= 14 days`** for High (`CVSS 7.0–8.9`), and **`<= 30 days`** for Medium.
   * **HARD GATE 3 (SLA Breach Escalation Gate):** Any Critical or `CISA KEV` vulnerability breaching its `7-day` window triggers a build freeze on non-security feature releases for that microservice and requires a Pillar 1 Risk Exception.
4. **Step 4 — CI/CD Pre-Release Security, Rollback & AI Egress `DLP` Gate (`Every Production Release`):**
   * Every production change is logged in `CICD_Change_Gate_Log` and evaluated against four automated pipeline checks before promotion.
   * **HARD GATE 4 (Production Promotion Block):** CI/CD pipelines automatically block deployment (`BLOCKED - GATE FAIL`) if any of the following fail: (a) Critical/High `SAST/SCA` vulnerabilities detected, (b) missing tested rollback plan/feature flag, (c) missing peer/2nd-line approval for `CIBS` changes, or (d) missing `PAN`/`PII` egress redaction proxy for AI/LLM integrations (`Pillar 6` link).

---

## 3. RACI & Accountability Matrix

| Pillar 2 Control Activity | CTO (`PCF-46`) | Platform & Payments Engineering (1st Line) | SecOps & AppSec | Head of ICT & InfoSec Risk (2nd Line) | Internal Audit (3rd Line) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Asset Inventory & `CIBS` Tagging Completeness** | **A** | **R** | **C** | **C (Oversight)** | **I** |
| **FIPS 140-3 HSM Key Ceremonies & Rotation** | **A** | **R** | **R** | **C (Witness)** | **I** |
| **Quarterly `PAM` Access Recertification (`90-Day`)** | **A** | **R (Entitlement Owners)** | **R (IAM Ops)** | **C (Challenge)** | **I** |
| **Critical / `CISA KEV` Vulnerability Patching (`<= 7d`)** | **A** | **R** | **R (Triage)** | **C (SLA Escalation)** | **I** |
| **CI/CD Pre-Release Security & `DLP` Gate Enforcement** | **A** | **R** | **R (Rule Config)** | **C (Gate Policy)** | **I** |

*(**R** = Responsible, **A** = Accountable, **C** = Consulted, **I** = Informed)*

---

## 4. Target Pillar 2 KPIs

| Metric / Outcome | Target Benchmark | Workbook & Formula Verification |
| :--- | :--- | :--- |
| **Critical (`CVSS >= 9.0`) & `CISA KEV` Patch SLA** | `>= 95.0%` remediated within `7 calendar days` | `Vulnerability_SLA_Tracker` & `Vuln_Change_Dashboard` |
| **Quarterly `PAM` Recertification Currency** | `100.0%` of privileged entitlements recertified within `90 days` | `Recertification Status` in `PAM_Access_Recertification` |
| **Cryptographic Key & Certificate Currency** | `0` expired TLS certificates or overdue HSM key rotations | `Key Status` in `Cryptographic_Key_Lifecycle` |
| **CI/CD Pre-Release Gate Integrity** | `0` high-risk changes promoted to production without passing all 4 gates | `Gate Verdict` in `CICD_Change_Gate_Log` |

---

## 5. Supporting Excel Registers
1. **[`pillar-02-asset-crypto-and-pam-scope.xlsx`](pillar-02-ict-protection-and-change-control/pillar-02-asset-crypto-and-pam-scope.xlsx)** — `Protection_Dashboard` · `ICT_Asset_CIBS_Inventory` · `Cryptographic_Key_Lifecycle` · `PAM_Access_Recertification`
2. **[`pillar-02-vuln-and-change-gate-tracker.xlsx`](pillar-02-ict-protection-and-change-control/pillar-02-vuln-and-change-gate-tracker.xlsx)** — `Vuln_Change_Dashboard` · `Vulnerability_SLA_Tracker` · `CICD_Change_Gate_Log`
