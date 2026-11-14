---
title: Pillar 5 — ICT Third-Party Risk Management, DORA RoI & Stressed Exit Plans
---

# Pillar 5: ICT Third-Party Risk Management, DORA RoI & Stressed Exit Plans
**Regulatory Basis:** DORA Chapter V (Articles 28–44) · EU Implementing Regulation 2024/2956 (EBA DPM 4.0 Register of Information) · EU Delegated Regulation 2024/1773 (CIFs) · Central Bank of Ireland (CBI) Cross-Industry Guidance on Outsourcing

---

## 1. What Pillar 5 Means in Practice
A Payment Institution can outsource cloud hosting, core ledger software, card tokenization, or fraud scoring to third-party providers—but **it can never outsource regulatory accountability to the Central Bank of Ireland (CBI)**.

Pillar 5 turns third-party risk management into a fast, enforceable operating workflow that solves three supervisory pain points:
1. **Error-Free Annual CBI Portal RoI Filings (`DORA Art. 28(3)` & `Implementing Reg. 2024/2956`):** Rather than scrambling each spring to assemble spreadsheets, the master Register of Information maintains live 20-character **LEIs**, ultimate parent undertakings, EBA service codes, and fourth-party mappings ready for **CBI Portal XBRL** upload.
2. **Pre-Signature DORA Article 30 Contractual Gating (`Art. 30(2)–(3)`):** Procurement and business teams get a fast-track `<= 7-day` review cycle, paired with a hard stop blocking signature unless security assurance (`SOC 2` / `ISO 27001` / `PCI-DSS`), **EU AI Act** guardrails, and mandatory DORA clauses (CBI audit rights, EEA data residency, and exit assistance) are verified.
3. **Fourth-Party Concentration & Tested Exit Strategies (`Art. 28(8)` & `Art. 29`):** Even across multiple SaaS vendors, underlying reliance on a single hyperscaler (`AWS eu-west-1`) creates hidden concentration risk. Every `CIF`-critical provider must have a documented exit mechanism and undergo an annual stressed exit tabletop or technical drill.

---

## 2. Regulatory Alignment Matrix (DORA & CBI Outsourcing Rules)

| Regulatory Anchor | Specific Supervisory Requirement | How Pillar 5 Operationalises It |
| :--- | :--- | :--- |
| **DORA Art. 28(3)** & **Implementing Reg. 2024/2956 (EBA DPM 4.0)** | Maintain and submit a complete Register of Information covering all ICT contractual arrangements, LEIs, parent entities, and service chains. | **`DORA_RoI_Master_Register`:** Validates 20-character LEI syntax automatically and maps contracts to EBA service codes and `CIBS` IDs. |
| **DORA Delegated Reg. 2024/1773** & **CBI Outsourcing Guidance** | Identify ICT services supporting Critical or Important Functions (`CIFs`) and apply heightened pre-contractual and ongoing scrutiny. | **`DORA_RoI_Master_Register` & `Vendor_DDQ_And_Art30_Gate`:** Flags `CIF Critical?` vendors and enforces enhanced due diligence and Board/PCF oversight. |
| **DORA Art. 29** & **CBI Outsourcing Guidance (*Concentration Risk*)** | Assess single-provider and fourth-party subcontractor concentration across critical payment rails. | **`Fourth_Party_Concentration`:** Aggregates primary vendors by underlying cloud/data-centre subcontractor and flags `> 50%` CIBS exposure. |
| **DORA Art. 30(2)–(3)** | Include mandatory contractual provisions: unrestricted CBI/audit access, EEA data locations, incident SLA support, termination triggers, and transition help. | **`Vendor_DDQ_And_Art30_Gate`:** Blocks contract execution (`BLOCKED - REMEDIATE`) if any Article 30 clause or security attestation is missing. |
| **DORA Art. 28(8)** & **CBI Outsourcing Guidance (*Exit Strategies*)** | Maintain actionable, documented, and periodically tested exit plans for all ICT services supporting Critical or Important Functions. | **`Stressed_Exit_Plan_Tracker`:** Tracks portability mechanisms, stressed migration windows (months), and annual drill currency (`<= 365 days`). |

---

## 3. End-to-End Vendor Lifecycle & Hard Decision Gates

1. **Step 1 — Business Intake & CIF / EU AI Act Triage (`Day 1`):**
   * Business owner submits a vendor intake request; 2nd Line ICT Risk determines whether the tool supports `CIBS-01`–`CIBS-05` (`CIF Critical?`) and whether it embeds AI functionality (`Annex III` high-risk vs. `Art. 50` chatbot vs. excluded fraud scoring).
2. **Step 2 — Security Due Diligence & Fourth-Party Mapping (`Days 2–4`):**
   * 2nd Line ICT Risk verifies `SOC 2 Type II`, `ISO 27001`, or `PCI-DSS v4.0 AoC` evidence, confirms EEA data residency, and records the provider's underlying cloud/data-centre subcontractor in **`Fourth_Party_Concentration`**.
3. **Step 3 — DORA Article 30 Contractual Gate (`Days 5–7`):**
   * Legal and 2nd Line ICT Risk verify mandatory DORA Article 30 clauses in **`Vendor_DDQ_And_Art30_Gate`**.
   * **Hard Gate:** No contract may be signed or production API keys provisioned until `Contract Gate Verdict` reads `APPROVED TO SIGN`.
4. **Step 4 — DORA RoI Ingestion & Annual Stressed Exit Drill:**
   * Signed contracts and verified 20-character LEIs are ingested into **`DORA_RoI_Master_Register`** for the annual **CBI Portal XBRL** filing.
   * Every `CIF`-critical provider is added to **`Stressed_Exit_Plan_Tracker`** and undergoes an annual tabletop or technical migration drill within `365 days`.

---

## 4. RACI & Accountability Matrix

| Third-Party & RoI Activity | Business Owner / Procurement | CTO / 1st Line Engineering | Legal & Compliance | Head of ICT & InfoSec Risk (2nd Line) | CEO (PCF-1) / Safeguarding (PCF-56) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Vendor Intake, Business Case & Commercials** | **R** | **C** | **I** | **I** | **A (Critical Spend)** |
| **Security DDQ, Fourth-Party & AI Triage** | **C** | **C** | **I** | **A / R** | **I** |
| **DORA Art. 30 Contractual Clause Negotiation** | **C** | **I** | **R** | **A (Risk Sign-Off)** | **I** |
| **DORA Register of Information (RoI) & CBI XBRL Filing** | **C** | **C** | **C** | **R** | **A (Portal Sign-Off)** |
| **Annual Stressed Exit Plan Tabletop / Tech Drill** | **C** | **R** | **I** | **A (Challenge)** | **I** |

*(**R** = Responsible, **A** = Accountable, **C** = Consulted, **I** = Informed)*

---

## 5. Target Third-Party Risk KPIs

| Metric / Outcome | Target Benchmark | How It Is Measured |
| :--- | :--- | :--- |
| **Vendor Security & Art. 30 Review Cycle** | `<= 7 business days` average turnaround | `Review Cycle (Days)` in `Vendor_DDQ_And_Art30_Gate` |
| **DORA RoI LEI & Schema Integrity** | `0` invalid LEIs or missing parent entities prior to CBI filing | `LEI Syntax Check` & `CBI Portal Status` in `DORA_RoI_Master_Register` |
| **DORA Article 30 Contract Compliance** | `100%` of new/renewed CIF contracts signed with full Art. 30 clauses | `Contract Gate Verdict` in `Vendor_DDQ_And_Art30_Gate` |
| **Stressed Exit Plan Drill Currency** | `100%` of CIF-critical vendors drilled within rolling `365 days` | `Drill Currency Status` in `Stressed_Exit_Plan_Tracker` |

---

## 6. Supporting Excel Registers
All active DORA Register of Information records, fourth-party concentration metrics, vendor due-diligence gates, and stressed exit drill logs are maintained across two companion Excel workbooks in this folder:

1. **[`pillar-05-dora-roi-and-concentration.xlsx`](pillar-05-dora-roi-and-concentration.xlsx)**
   * **`RoI_Concentration_Dashboard`:** Executive KPI cards and annual ICT spend exposure chart.
   * **`DORA_RoI_Master_Register`:** EBA DPM 4.0 master register with automated 20-character LEI validation and `CIF` flags.
   * **`Fourth_Party_Concentration`:** Subcontractor aggregation matrix flagging `> 50%` single-hyperscaler concentration.
2. **[`pillar-05-vendor-ddq-art30-and-exit.xlsx`](pillar-05-vendor-ddq-art30-and-exit.xlsx)**
   * **`TPRM_Governance_Dashboard`:** Onboarding SLA KPIs and stressed migration window chart.
   * **`Vendor_DDQ_And_Art30_Gate`:** Pre-signature security, EU AI Act, and DORA Article 30 contractual compliance gate.
   * **`Stressed_Exit_Plan_Tracker`:** Portability mechanisms, migration windows, and annual exit drill currency log.
