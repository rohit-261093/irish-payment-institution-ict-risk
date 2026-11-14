---
title: Irish Regulated Payment Institution (PI/EMI) — 6-Pillar ICT Risk, Operational Resilience & EU AI Act Blueprint
---

# Irish Regulated Payment Institution (PI/EMI)
### 6-Pillar Operational Resilience, ICT Risk & EU AI Act Operating System

An operator-first governance and execution blueprint demonstrating how a **Central Bank of Ireland (CBI)–authorised Payment Institution** operationalises **DORA (Regulation (EU) 2022/2554, Chapters II–V)**, **CBI Cross-Industry Operational Resilience & Outsourcing Guidance**, **CBI Individual Accountability Framework (IAF/SEAR)**, and the **EU AI Act (Regulation (EU) 2024/1689) / Ireland's Regulation of Artificial Intelligence Act 2026** across real-time SEPA Instant, card acquiring, and cross-border payment rails.

Built from a **Head of Security / Head of ICT & InfoSec Risk** perspective, this repository moves beyond static policy statements. Each pillar pairs a **plain-English operating guide (`README.md`)**—defining end-to-end workflows, hard engineering and contractual decision gates, RACI accountability, and target KPIs—with **12 formula-driven Excel registers (`.xlsx`)** ready for Board Risk Committee reporting, internal audit challenge, and CBI supervisory inspections.

---

## 1. Repository Architecture & File Tree

```text
irish-payment-institution-ict-risk/
├── index.md                                                             # Master 6-pillar operating architecture & supervisory matrix
├── pillar-01-governance-and-impact-tolerances/                          # [COMPLETE] DORA Ch. II, CBI OpRes & IAF/SEAR
│   ├── README.md
│   ├── pillar-01-cibs-impact-tolerances.xlsx
│   └── pillar-01-board-governance-and-harm-calibration.xlsx
├── pillar-02-ict-protection-and-change-control/                         # [COMPLETE] DORA Art. 8–9, Crypto, PAM & Change Gates
│   ├── README.md
│   ├── pillar-02-asset-crypto-and-pam-scope.xlsx
│   └── pillar-02-vuln-and-change-gate-tracker.xlsx
├── pillar-03-incident-response-and-cbi-reporting/                       # [COMPLETE] DORA Ch. III, RTS 2024/1772 & 4h CBI Clock
│   ├── README.md
│   ├── pillar-03-dora-incident-cbi-clock.xlsx
│   └── pillar-03-crisis-comms-and-capa-log.xlsx
├── pillar-04-resilience-testing-and-tiber-ie/                           # [COMPLETE] DORA Ch. IV, BCDR Drills & TIBER-IE TLPT
│   ├── README.md
│   ├── pillar-04-resilience-testing-scorecard.xlsx
│   └── pillar-04-pentest-and-tiber-ie-tracker.xlsx
├── pillar-05-third-party-risk-and-dora-roi/                             # [COMPLETE] DORA Ch. V, EBA DPM 4.0 RoI & Exit Plans
│   ├── README.md
│   ├── pillar-05-dora-roi-and-concentration.xlsx
│   └── pillar-05-vendor-ddq-art30-and-exit.xlsx
└── pillar-06-eu-ai-act-governance/                                      # [COMPLETE] EU AI Act Art. 26 Deployer & Irish AI Act 2026
    ├── README.md
    ├── pillar-06-eu-ai-act-inventory-and-fria.xlsx
    └── pillar-06-vendor-ai-assurance-and-llm-dlp.xlsx
```

---

## 2. Executive Design Philosophy: Why This Operating System Works

Regulated Payment Institutions in Ireland face overlapping enforcement across **DORA** (in force since January 2025), the **CBI Cross-Industry Operational Resilience Guidance**, and **Ireland's Regulation of Artificial Intelligence Act 2026** (which designates the CBI as market surveillance authority for AI in financial services). Rather than running fragmented compliance silos, this 6-pillar architecture enforces four unifying engineering principles:

1. **External Customer Harm Anchors Every Technical Control:** Every ICT asset, cryptographic key, vulnerability SLA, failover drill, vendor contract, and AI API is tagged directly to a Board-approved **Critical or Important Business Service (`CIBS-01` to `CIBS-05`)**. When an outage or cyber event occurs, engineering knows within minutes whether a `30-minute` SEPA Instant impact tolerance is threatened.
2. **Deterministic Hard Gates Over Passive Checklists:** Policies do not stop bad deployments or unvetted vendors; automated gates do. This framework embeds hard operational stops across CI/CD pipelines (Pillar 2), the 45-minute DORA incident classification triage (Pillar 3), 60-day TIBER-IE Purple-Team replay verification (Pillar 4), pre-signature `Article 30` contract reviews (Pillar 5), and pre-go-live `Article 26 / 27` AI Deployer gates (Pillar 6).
3. **100% Third-Party AI Deployer Precision:** Because the Payment Institution **does not train or develop proprietary AI models in-house**, Pillar 6 eliminates unnecessary model-training bureaucracy and focuses rigorously on **EU AI Act Article 26 Deployer obligations**—preventing accidental `Article 25` reclassification as a Provider, separating excluded fraud/AML APIs (`Annex III Point 5(b)`) from high-risk credit/biometric APIs, enforcing `15–60 minute` human-in-the-loop override SLAs, and blocking unsanctioned Shadow AI at the network proxy.
4. **Single-Source-of-Truth Supervisory Telemetry:** Every workbook contains an executive dashboard driven by dynamic formulas (`COUNTIFS`, `AVERAGE`, `INDEX/MATCH`, automated SLA countdowns, and RAG conditional formatting) so 1st Line Engineering, 2nd Line ICT Risk, and Pre-Approval Controlled Function (`PCF`) holders view identical, audit-verifiable metrics.

---

## 3. Master 6-Pillar Operating Matrix

| Pillar & Operating Guide | Primary Regulatory Anchors | End-to-End Workflow & Hard Decision Gates | Target Outcomes & Quantitative KPIs | Companion Excel Registers (`.xlsx`) |
| :--- | :--- | :--- | :--- | :--- |
| **[Pillar 1: Resilience Governance & Impact Tolerances](pillar-01-governance-and-impact-tolerances/README.md)** | • **DORA Ch. II (Art. 5–6)**<br>• **CBI OpRes Guidance (G1–G7)**<br>• **CBI IAF / SEAR & PCF Regime** | 1. External `CIBS` vs. internal `CIF` classification<br>2. End-to-end dependency mapping (apps, AWS AZs, payment schemes, vendors)<br>3. Time-bucket harm calibration (`15m`, `30m`, `2h`, `4h`, `24h`)<br>4. Annual Board RTO/RPO approval & ICT-SAT maturity review<br>5. **Hard Gate:** 90-day Risk Exception expiry & Board escalation | • SEPA Instant (`CIBS-01`) RTO `<= 30m` & RPO `0` txn loss<br>• `0` expired risk exceptions without formal Board Risk Committee renewal<br>• `100%` annual Board/staff DORA & `Art. 4` AI literacy training completion<br>• `100%` quarterly PCF attestation currency | • [`pillar-01-cibs-impact-tolerances.xlsx`](pillar-01-governance-and-impact-tolerances/pillar-01-cibs-impact-tolerances.xlsx)<br>• [`pillar-01-board-governance-and-harm-calibration.xlsx`](pillar-01-governance-and-impact-tolerances/pillar-01-board-governance-and-harm-calibration.xlsx) |
| **[Pillar 2: ICT Protection & Change Control](pillar-02-ict-protection-and-change-control/README.md)** | • **DORA Art. 8–9**<br>• **DORA RTS on ICT Risk (2024/1774)**<br>• **CBI Cross-Industry Cyber Guidance** | 1. Asset-to-`CIBS` criticality tagging<br>2. FIPS 140-3 HSM cryptographic key lifecycle & 90-day PAM recertification<br>3. Risk-tiered CVSS / CISA KEV vulnerability patching<br>4. **Hard Gate:** Pre-release CI/CD SAST/SCA, rollback proof & AI egress DLP checks | • Critical (`CVSS >= 9.0`) & CISA KEV vulnerabilities patched `<= 7 days` (`>= 95%` SLA)<br>• `100%` quarterly PAM access recertification across HSMs, cloud root & bank portals<br>• `0` high-risk production releases deployed without rollback plan & DLP check | • [`pillar-02-asset-crypto-and-pam-scope.xlsx`](pillar-02-ict-protection-and-change-control/pillar-02-asset-crypto-and-pam-scope.xlsx)<br>• [`pillar-02-vuln-and-change-gate-tracker.xlsx`](pillar-02-ict-protection-and-change-control/pillar-02-vuln-and-change-gate-tracker.xlsx) |
| **[Pillar 3: Incident Response & CBI 4-Hour Clock](pillar-03-incident-response-and-cbi-reporting/README.md)** | • **DORA Ch. III (Art. 17–23)**<br>• **DORA RTS 2024/1772** (Major Incident Criteria)<br>• **CBI OpRes Guidance (G11–G13)** | 1. Detection (`T+0`) & containment<br>2. **Hard Gate (`<= 45m`):** Deterministic EU RTS threshold scoring (clients, value, duration, data loss)<br>3. **`<= 4h`:** CBI Portal Initial Notification (`<= 24h` from detection)<br>4. **`<= 72h`:** Intermediate Report & `Art. 19(3)` client notice<br>5. **`<= 30d`:** Root Cause Analysis (`RCA`) & `CAPA` closure | • Mean Time to Classify (`MTTC`) `<= 45 minutes` from detection<br>• `100%` on-time `4-hour`, `72-hour`, and `30-day` CBI Portal regulatory filings<br>• `100%` monthly `Art. 8(2)` aggregation of recurring minor incidents<br>• `0` overdue `CAPA` actions beyond 30-day target | • [`pillar-03-dora-incident-cbi-clock.xlsx`](pillar-03-incident-response-and-cbi-reporting/pillar-03-dora-incident-cbi-clock.xlsx)<br>• [`pillar-03-crisis-comms-and-capa-log.xlsx`](pillar-03-incident-response-and-cbi-reporting/pillar-03-crisis-comms-and-capa-log.xlsx) |
| **[Pillar 4: Resilience Testing & TIBER-IE TLPT](pillar-04-resilience-testing-and-tiber-ie/README.md)** | • **DORA Ch. IV (Art. 24–27)**<br>• **TIBER-IE Framework** (CBI)<br>• **CBI OpRes Guidance (G8–G9)** | 1. Annual risk-based resilience test schedule covering all `CIBS`<br>2. **Hard Gate:** `Art. 27` external tester independence & CREST/TIBER vetting<br>3. Quarterly BCDR active-active failover drills<br>4. TIBER-IE red-team simulation<br>5. **Hard Gate (`<= 60d`):** Critical/High finding fix & Purple-Team replay | • Actual failover RTO `<= 75%` of Board-approved Impact Tolerance<br>• `100%` of TIBER-IE & Critical/High pen-test findings remediated & Purple-Team replayed `<= 60 days`<br>• `100%` of external testers vetted against `Art. 27` independence criteria | • [`pillar-04-resilience-testing-scorecard.xlsx`](pillar-04-resilience-testing-and-tiber-ie/pillar-04-resilience-testing-scorecard.xlsx)<br>• [`pillar-04-pentest-and-tiber-ie-tracker.xlsx`](pillar-04-resilience-testing-and-tiber-ie/pillar-04-pentest-and-tiber-ie-tracker.xlsx) |
| **[Pillar 5: Third-Party Risk & DORA RoI](pillar-05-third-party-risk-and-dora-roi/README.md)** | • **DORA Ch. V (Art. 28–44)**<br>• **EBA DPM 4.0 RoI** (ITS 2024/2956)<br>• **CBI Cross-Industry Outsourcing** | 1. Vendor intake & `CIF` criticality triage<br>2. Security DDQ & 4th-party hyperscaler concentration mapping<br>3. **Hard Gate:** `Art. 30` mandatory contract clause sign-off<br>4. EBA DPM 4.0 RoI 20-char LEI validation for CBI XBRL filing<br>5. Annual stressed exit tabletop drill | • Vendor security & `Art. 30` contract review turnaround `<= 7 business days`<br>• `0` invalid 20-character LEIs prior to annual CBI Portal XBRL RoI submission<br>• `100%` of `CIF`-critical vendors exit-drilled within rolling `365 days` | • [`pillar-05-dora-roi-and-concentration.xlsx`](pillar-05-third-party-risk-and-dora-roi/pillar-05-dora-roi-and-concentration.xlsx)<br>• [`pillar-05-vendor-ddq-art30-and-exit.xlsx`](pillar-05-third-party-risk-and-dora-roi/pillar-05-vendor-ddq-art30-and-exit.xlsx) |
| **[Pillar 6: EU AI Act Deployer Governance](pillar-06-eu-ai-act-governance/README.md)** | • **EU AI Act (Reg. 2024/1689)** (`Art. 4, 5, 25, 26, 27, 50, 73`)<br>• **Ireland Regulation of AI Act 2026**<br>• **CBI Feb 2026 Supervisory Outlook** | 1. Third-party AI intake (`0` in-house trained models) & `Art. 25` anti-rebranding check<br>2. Statutory triage (`Annex III Point 5(b)` fraud/AML carve-out vs. high-risk credit/biometric)<br>3. **Hard Gate:** `Art. 26` vendor instructions, `DPIA + Art. 27 FRIA` & `Art. 50` UI notice verification<br>4. Quarterly vendor bias/audit pack review & CASB Shadow AI proxy blocking | • `100%` of third-party AI APIs inventoried & classified prior to production activation<br>• `100%` of `Annex III` high-risk APIs covered by signed FRIAs & human review queues (`>= 98%` SLA)<br>• `100%` quarterly vendor bias/conformity audit pack currency<br>• `0` unsanctioned GenAI tools permitted to process customer PII/PAN | • [`pillar-06-eu-ai-act-inventory-and-fria.xlsx`](pillar-06-eu-ai-act-governance/pillar-06-eu-ai-act-inventory-and-fria.xlsx)<br>• [`pillar-06-vendor-ai-assurance-and-llm-dlp.xlsx`](pillar-06-eu-ai-act-governance/pillar-06-vendor-ai-assurance-and-llm-dlp.xlsx) |

---

## 4. Cross-Pillar Operational Integration (How the 6 Pillars Interlock)

No pillar operates in isolation. Data flows systematically across the workbooks to prevent duplicate registers and blind spots:

* **Pillar 1 → Pillars 2, 3, 4, 5 & 6 (`CIBS` Criticality Spine):** `CIBS-01` (SEPA Instant), `CIBS-02` (Card Acquiring), `CIBS-03` (Safeguarding Ledger), `CIBS-04` (Customer Portal & Onboarding), and `CIBS-05` (Merchant Working Capital) defined in Pillar 1 serve as the primary foreign keys across every asset, incident, BCDR test, vendor contract, and AI API in Pillars 2–6.
* **Pillar 2 ↔ Pillar 6 (`AI Egress DLP & Change Gates`):** Pre-release CI/CD gates in Pillar 2 enforce API secret/PAN redaction proxies and Zero-Data-Retention (`ZDR`) EU endpoint checks for the SaaS GenAI tools governed in Pillar 6.
* **Pillar 3 ↔ Pillar 6 (`DORA 4-Hour Clock & EU AI Act Art. 73`):** If a third-party AI system in Pillar 6 suffers a serious malfunction—such as a fraud-scoring API falsely blocking `> 10%` of live SEPA Instant traffic or an eKYC API causing discriminatory onboarding rejections—the `60-second` API kill-switch triggers an immediate escalation into **Pillar 3's 45-minute DORA triage and 4-hour CBI Portal notification clock**.
* **Pillar 4 ↔ Pillar 5 (`Vendor Failover & Stressed Exit Testing`):** Pillar 4's quarterly BCDR failover drills validate the Recovery Time Objectives (`RTOs`) of `CIF`-critical ICT vendors catalogued in Pillar 5's DORA Register of Information (`AWS`, `ClearBank`, `SentinelAI`, `VeriID`).
* **Pillar 5 ↔ Pillar 6 (`DORA RoI & Third-Party AI Supply Chain`):** Every external AI vendor in Pillar 6 (`ICT-004`, `ICT-005`, `ICT-006`, `VND-AI-02`) is anchored to a validated 20-character LEI, `Article 30` contract, and concentration risk score in Pillar 5's EBA DPM 4.0 Register of Information.

---

## 5. Central Bank of Ireland (CBI) Supervisory & Audit Readiness Map

| Supervisory Inspection / Statutory Filing | Governing Pillars | Ready-to-Inspect Artefacts & Evidence Packs |
| :--- | :--- | :--- |
| **CBI Operational Resilience Inspection & ICT Self-Assessment Tool (`ICT-SAT`)** | **Pillars 1, 2, 3, 4** | Board-approved `CIBS` dependency and time-bucket harm calibration matrices, annual `ICT-SAT` maturity self-assessment log, quarterly BCDR failover scorecards, and 90-day risk exception register. |
| **CBI Portal Major ICT Incident Notifications (`DORA Art. 19` / `RTS 2024/1772`)** | **Pillars 1, 3, 6** | Deterministic 45-minute classification calculator, timestamped `4-hour` Initial / `72-hour` Intermediate / `30-day` Final CBI Portal submission logs, `Art. 19(3)` client communication templates, and `Art. 8(2)` minor incident aggregation logs. |
| **TIBER-IE Threat-Led Penetration Testing (`TLPT`) & Vulnerability Assurance** | **Pillars 2, 4** | Annual risk-based resilience testing programme, `Art. 27` external tester independence attestations, TIBER-IE red-team scope & threat intelligence mapping, and 60-day Purple-Team replay closure evidence. |
| **CBI Portal Annual DORA Register of Information (`EBA DPM 4.0 XBRL`)** | **Pillar 5** | Master ICT third-party contractual arrangement register (`B_01.01` to `B_07.01` data points), automated 20-character LEI validation checks, parent undertaking hierarchies, fourth-party cloud concentration scores, and rolling 365-day exit drill logs. |
| **CBI AI Market Surveillance (*Regulation of Artificial Intelligence Act 2026*)** | **Pillars 1, 5, 6** | Board & staff `Art. 4` AI literacy completion records, central third-party AI Deployer inventory (`0` in-house trained models), `Art. 27` FRIAs, `Art. 50` chatbot UI transparency proofs, quarterly vendor bias/conformity audit packs, and `15–60 min` human override logs. |

---

## 6. Governance Accountability Matrix (`IAF / SEAR` & Three Lines of Defence)

Under the **CBI Individual Accountability Framework (`IAF/SEAR`)** and **Ireland's Regulation of Artificial Intelligence Act 2026**, governance ownership is explicitly assigned across Pre-Approval Controlled Functions (`PCFs`) and the Three Lines of Defence:

| Governance Domain | Board Risk Committee (`INEDs`) | CEO (`PCF-1`) & CRO (`PCF-14`) | CTO (`PCF-46`) & Engineering (1st Line) | MLRO / Head of Compliance (`PCF-52`) | Head of ICT & InfoSec Risk (2nd Line) | Internal Audit (3rd Line) |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **Impact Tolerances, Risk Appetite & `ICT-SAT` Approval** | **A** | **C** | **C** | **C** | **R** | **I** |
| **Asset Protection, Crypto, PAM & CI/CD Security Gates** | **I** | **I** | **R / A**
