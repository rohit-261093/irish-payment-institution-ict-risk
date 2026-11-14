---
title: Irish Regulated Payment Institution (PI/EMI) — ICT Risk, Operational Resilience & AI Governance Blueprint
---

# Irish Regulated Payment Institution (PI/EMI)
### 6-Pillar Operational Resilience, ICT Risk & EU AI Act Operating System

An operator-first governance and execution blueprint demonstrating how a **Central Bank of Ireland (CBI)–authorised Payment Institution** operationalises **DORA (Chapters II–V)**, **CBI Cross-Industry Operational Resilience & Outsourcing Guidance**, **CBI Individual Accountability Framework (IAF/SEAR)**, and the **EU AI Act / Ireland's Regulation of Artificial Intelligence Act 2026** across real-time SEPA Instant and payment rails.

Built from a **Head of Security / Head of ICT & InfoSec Risk** perspective, each pillar pairs a **plain-English operating guide (`README.md`)**—defining end-to-end workflows, hard decision gates, RACI accountability, and target KPIs—with **formula-driven Excel registers (`.xlsx`)** ready for Board Risk Committee reporting and CBI supervisory inspections.

---

## 1. Repository Architecture

```text
irish-payment-institution-ict-risk/
├── index.md                                                             # Master 6-pillar operating matrix & navigation
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
└── pillar-06-eu-ai-act-governance/                                      # [COMPLETE] EU AI Act (Reg. 2024/1689 Art. 26 Deployer)
    ├── README.md
    ├── pillar-06-eu-ai-act-inventory-and-fria.xlsx
    └── pillar-06-vendor-ai-assurance-and-llm-dlp.xlsx
