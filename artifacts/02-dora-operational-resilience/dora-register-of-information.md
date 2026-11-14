---
title: DORA Register of Information (RoI) & Critical ICT Exit Strategy
---

# DORA Register of Information (RoI) & Critical ICT Third-Party Exit Plan
**Entity Profile:** Irish-Authorised Payment Institution (PI/EMI) | **Entity LEI:** `549300SAMPLEIRISHPI01`  
**Owner:** Head of ICT & InfoSec Risk (2nd Line of Defence)  
**Regulatory Basis:** DORA Article 28(3), Commission Implementing Regulation (EU) 2024/2956, & CBI Cross-Industry Guidance on Outsourcing  

---

## 1. Executive Governance & CBI Portal Submission Lifecycle
Under **DORA Article 28(3)**, the firm maintains a continuous, machine-validated Register of Information covering **all contractual arrangements** for ICT services—not solely critical providers—aligned with the **EBA Data Point Model (DPM 4.0)** and exported in **XBRL OIM-CSV** format for annual upload to the **Central Bank of Ireland (CBI) Portal** (1–31 March submission window).

### Data Quality & EBA Validation Controls (Zero-Rejection Standard)
To prevent EBA content-review and April data-quality resubmissions, procurement and 2nd Line ICT Risk enforce four hard ingestion gates before onboarding any ICT vendor:
1. **Verified Legal Identifiers:** Every ICT Third-Party Service Provider (TPP) and its **Ultimate Parent Undertaking** must have a verified **LEI** (or valid EU-ID / third-country equivalent). Dummy or generic strings (e.g., `9999999DUMMY` or `N/A`) are blocked at contract intake.
2. **Function-to-Asset Lineage:** Every contract is mapped directly to supported business functions (`B_06.01`) and classified for criticality (`Critical or Important Function [CIF]` vs. `Non-CIF`) using CBI outsourcing criticality criteria.
3. **Subcontracting Chain Visibility (`B_05.01` / `B_05.02`):** Mandatory contractual disclosure of fourth-party material subcontractors underpinning CIFs, including data storage/processing jurisdictions.
4. **January Dry-Run Validation:** Full XBRL schema validation and Board Risk Committee sign-off completed by **31 January** each year ahead of the March CBI Portal window.

---

## 2. Sample Register of Information (CIF & Material ICT Dependencies)

| Contract Ref | ICT Provider & Ultimate Parent | Provider LEI / ID | ICT Service Type | Supported Business Function | CIF Status | Subcontractors (4th Party) & Data Location | Substitutability & Exit Tier |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **ICT-2026-001** | **CoreLedger Cloud Ltd** *(Parent: FinCore Holdings plc)* | `213800CORELEDGER001` | Core Payment Ledger & Safeguarding Reconciliation SaaS | SEPA / SEPA Instant Clearing & Safeguarding Ledger | **Yes (CIF)** | AWS (`eu-west-1` Dublin primary; `eu-central-1` Frankfurt DR) | **Low Substitutability** — 9-month stressed exit plan; escrow + ISO 20022 data export |
| **ICT-2026-002** | **Amazon Web Services EMEA SARL** *(Parent: Amazon.com, Inc.)* | `549300AWSEMEA000009` | Cloud IaaS / PaaS & KMS Hosting | Payment API Gateway, Microservices & Telemetry | **Yes (CIF)** | Direct Hyperscaler (`eu-west-1` Ireland & `eu-central-1` Germany) | **Medium Substitutability** — 6-month container/IaC migration to secondary EU cloud |
| **ICT-2026-003** | **EuroPay Card Vault & HSM Corp** *(Parent: EuroPay Group SA)* | `529900EUROPAYHSM002` | PCI-DSS v4.0 Tokenization Vault & Cloud HSM | Card Issuing, Authorization & Cryptographic Signing | **Yes (CIF)** | Equinix LD5/DB1 Data Centres (Ireland / EU) | **Low Substitutability** — 12-month dual-BIN/token migration; tested key ceremony export |
| **ICT-2026-004** | **SentinelAI Fraud Systems Inc.** *(Parent: SentinelAI Corp)* | `549300SENTINELAI004` | Real-Time Transaction Fraud & AML Scoring API | Pre-Settlement Fraud & Sanctions Screening | **Yes (CIF)** | Google Cloud (`europe-west1` Belgium) | **Medium Substitutability** — 90-day rules-engine fallback + secondary fraud vendor warm standby |
| **ICT-2026-005** | **ClearComms Support AI Ltd** *(Parent: ClearComms Group)* | `213800CLEARCOMMS005` | Customer Dispute Chat & Ticketing Platform | Customer Support & PSD3 Dispute Handling | **No (Non-CIF)** | Azure (`northeurope` Ireland) | **High Substitutability** — 30-day standard SaaS offboarding & CSV export |

---

## 3. Critical ICT Exit Strategy & Transition Blueprint (`ICT-2026-001` & `003`)

In line with **DORA Article 28(8)** and CBI
