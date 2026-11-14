# Irish Regulated Payment Institution (PI/EMI) — ICT Risk, Operational Resilience & EU AI Act Blueprint

An operator-first governance, risk, and compliance (GRC) operating system demonstrating how a **Central Bank of Ireland (CBI)–authorised Payment Institution** operationalises **DORA (Regulation (EU) 2022/2554)**, **CBI Cross-Industry Operational Resilience & Outsourcing Guidance**, **CBI Individual Accountability Framework (IAF/SEAR)**, and the **EU AI Act / Ireland's Regulation of Artificial Intelligence Act 2026**.

Designed from a **Head of Security / Head of ICT & InfoSec Risk** perspective, this repository replaces static policy binders with **6 executable operating guides** and **12 formula-driven Excel registers (`.xlsx`)** ready for Board Risk Committee reporting and CBI supervisory inspections.

---

## Why This Blueprint Exists

Regulated Payment Institutions in Ireland face overlapping supervisory scrutiny across real-time payment rails (SEPA Instant, card acquiring, safeguarding ledgers) and third-party AI APIs. Rather than managing compliance in disconnected silos, this repository enforces four practical operating principles:

1. **Customer Harm Anchors Every Control:** Every ICT asset, cryptographic key, vulnerability SLA, failover drill, vendor contract, and AI API maps directly to a Board-approved **Critical or Important Business Service (`CIBS-01` to `CIBS-05`)**.
2. **Hard Decision Gates Over Passive Checklists:** Automated operational gates prevent unvetted changes, expired risk exceptions, missing `Article 30` contract clauses, and unapproved AI deployments from reaching production.
3. **100% Third-Party AI Deployer Precision:** Because the firm **does not train or develop proprietary AI models in-house**, Pillar 6 eliminates provider-level model-training overhead and focuses strictly on **EU AI Act Article 26 Deployer obligations**—separating excluded fraud/AML APIs (`Annex III Point 5(b)`) from high-risk credit/biometric APIs, enforcing `15–60 min` human override SLAs, and blocking Shadow AI at the proxy.
4. **Audit-Ready Supervisory Telemetry:** All 12 Excel workbooks include executive dashboards driven by live formulas (`COUNTIFS`, `AVERAGE`, automated SLA countdowns, and RAG conditional formatting).

---

## Repository Structure

```text
├── index.md                                                             # Master 6-pillar architecture & supervisory mapping
├── README.md                                                            # Repository overview & quick-start guide
├── pillar-01-governance-and-impact-tolerances/                          # DORA Ch. II, CBI OpRes & IAF/SEAR
│   ├── README.md
│   ├── pillar-01-cibs-impact-tolerances.xlsx
│   └── pillar-01-board-governance-and-harm-calibration.xlsx
├── pillar-02-ict-protection-and-change-control/                         # DORA Art. 8–9, Crypto, PAM & Change Gates
│   ├── README.md
│   ├── pillar-02-asset-crypto-and-pam-scope.xlsx
│   └── pillar-02-vuln-and-change-gate-tracker.xlsx
├── pillar-03-incident-response-and-cbi-reporting/                       # DORA Ch. III, RTS 2024/1772 & 4h CBI Clock
│   ├── README.md
│   ├── pillar-03-dora-incident-cbi-clock.xlsx
│   └── pillar-03-crisis-comms-and-capa-log.xlsx
├── pillar-04-resilience-testing-and-tiber-ie/                           # DORA Ch. IV, BCDR Drills & TIBER-IE TLPT
│   ├── README.md
│   ├── pillar-04-resilience-testing-scorecard.xlsx
│   └── pillar-04-pentest-and-tiber-ie-tracker.xlsx
├── pillar-05-third-party-risk-and-dora-roi/                             # DORA Ch. V, EBA DPM 4.0 RoI & Exit Plans
│   ├── README.md
│   ├── pillar-05-dora-roi-and-concentration.xlsx
│   └── pillar-05-vendor-ddq-art30-and-exit.xlsx
└── pillar-06-eu-ai-act-governance/                                      # EU AI Act Art. 26 Deployer & Irish AI Act 2026
    ├── README.md
    ├── pillar-06-eu-ai-act-inventory-and-fria.xlsx
    └── pillar-06-vendor-ai-assurance-and-llm-dlp.xlsx
```

---

## The 6 Operational Pillars at a Glance

| Pillar | Regulatory Scope | Key Deliverables & Registers |
| :--- | :--- | :--- |
| **[01. Resilience Governance & Impact Tolerances](pillar-01-governance-and-impact-tolerances/README.md)** | **DORA Ch. II**, **CBI OpRes**, & **IAF/SEAR** | `CIBS` vs. `CIF` inventory, end-to-end dependency mapping, time-bucket harm calibration (`15m`–`24h`), Board RTO/RPO approvals, and 90-day risk exception gates. |
| **[02. ICT Protection & Change Control](pillar-02-ict-protection-and-change-control/README.md)** | **DORA Art. 8–9** & **CBI Cyber Guidance** | Asset-to-`CIBS` tagging, FIPS 140-3 HSM key lifecycle, quarterly PAM recertification, CVSS/CISA KEV patch SLAs (`<= 7d`), and CI/CD pre-release security/DLP gates. |
| **[03. Incident Response & CBI 4-Hour Clock](pillar-03-incident-response-and-cbi-reporting/README.md)** | **DORA Ch. III** & **RTS 2024/1772** | `45-minute` deterministic EU RTS threshold triage, `4-hour` CBI Portal Initial Notice, `72-hour` Intermediate Report, `Art. 19(3)` client notices, and `30-day` RCA/CAPA tracking. |
| **[04. Resilience Testing & TIBER-IE TLPT](pillar-04-resilience-testing-and-tiber-ie/README.md)** | **DORA Ch. IV** & **TIBER-IE Framework** | Annual risk-based test programme, `Art. 27` tester independence vetting, quarterly BCDR failover scorecards (`<= 75%` of RTO), and `60-day` TIBER-IE Purple-Team replay closure. |
| **[05. Third-Party Risk & DORA RoI](pillar-05-third-party-risk-and-dora-roi/README.md)** | **DORA Ch. V** & **EBA DPM 4.0 (XBRL)** | Vendor security DDQs, `Article 30` contract gates, EBA DPM 4.0 Register of Information with 20-char LEI validation, 4th-party concentration tracking, and annual exit drills. |
| **[06. EU AI Act Deployer Governance](pillar-06-eu-ai-act-governance/README.md)** | **EU AI Act Art. 26** & **Irish AI Act 2026** | Third-party AI Deployer register (`0` in-house trained models), `Annex III` vs. fraud/AML carve-out classification, `Art. 27` FRIAs, `Art. 50` disclosures, quarterly vendor audit packs, and GenAI DLP. |

---

## How to Use This Repository

1. **Start with [`index.md`](index.md)** for the master cross-pillar integration architecture, CBI supervisory inspection mapping, and `IAF/SEAR` Three Lines of Defence accountability matrix.
2. **Open any Pillar folder (`pillar-01` through `pillar-06`)** to read its step-by-step operating workflow, RACI table, and target KPIs in `README.md`.
3. **Download and inspect the companion `.xlsx` workbooks** in Excel or LibreOffice to review the live dashboards, RAG conditional formatting, and supervisory tracking registers.

---

## Regulatory & Industry References
* **Central Bank of Ireland (CBI):** *Cross-Industry Guidance on Operational Resilience*, *Cross-Industry Guidance on Outsourcing*, *ICT Self-Assessment Tool (`ICT-SAT`)*, *TIBER-IE Framework*, and *Regulatory & Supervisory Outlook (February 2026)*.
* **European Union & Irish Statutory Law:** *Digital Operational Resilience Act (DORA — Regulation (EU) 2022/2554)*, *EBA DORA Register of Information Data Point Model (`DPM 4.0`)*, *EU Artificial Intelligence Act (Regulation (EU) 2024/1689)*, and *Ireland's Regulation of Artificial Intelligence Act 2026 (Act 31 of 2026)*.
* **Community Benchmark:** [Taimur Ijlal — AI Governance Repository](https://github.com/taimurijlal/AIGovernance).
