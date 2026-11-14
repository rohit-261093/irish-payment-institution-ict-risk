---

## Quick Navigation (Interview Walkthrough)
* [1. Irish Regulatory & Supervisory Alignment](#1-irish-regulatory--supervisory-alignment)
* [2. End-to-End Payment & AI Security Architecture](#2-end-to-end-payment--ai-security-architecture)
* [3. Governance Artifacts & Runbooks](#3-governance-artifacts--runbooks)
* [4. Executive Risk Trade-Offs (Head of ICT Risk Lens)](#4-executive-risk-trade-offs-head-of-ict-risk-lens)

---

## 1. Irish Regulatory & Supervisory Alignment

| Regulatory Pillar | Irish / EU Instrument | Head of ICT & InfoSec Risk Accountability |
| :--- | :--- | :--- |
| **Digital Operational Resilience** | **DORA** (Reg. (EU) 2022/2554) & **CBI ICT-SAT** | Management-body approved ICT Risk Framework, **Register of Information (RoI)** for ICT third parties, 4-hour/72-hour CBI major incident reporting, and **TIBER-IE** TLPT readiness. |
| **Payments Licensing & Fraud** | **PSD2** → **PSD3 / PSR** Transition | Strong Customer Authentication (SCA), **Verification of Payee (VoP)** IBAN/name checks, APP fraud monitoring, and safeguarding account resilience under unified PI/EMI rules. |
| **AI & Algorithmic Governance** | **EU AI Act** (Reg. (EU) 2024/1689) | Enterprise AI inventory, **Annex III** high-risk classification (separating credit scoring from excluded fraud-detection models), **Art. 50** chatbot transparency, and human override controls. |
| **Cardholder Data Security** | **PCI-DSS v4.0** | Cardholder Data Environment (CDE) isolation via hosted tokenization vaults, HSM key management, and client-side script integrity. |
| **Executive Accountability** | **CBI IAF / SEAR** | Clear Three Lines of Defence mapping linking ICT & InfoSec risk ownership to Pre-Approval Controlled Functions (PCFs) and Board Risk Committees. |

---

## 2. End-to-End Payment & AI Security Architecture

```mermaid
flowchart LR
    subgraph Channels["1. Customer & Merchant Channels"]
        APP["Mobile Banking App<br/>(Device Binding + Biometric SCA)"]
        API["Merchant / Partner API<br/>(mTLS + OAuth2 + Rate Limiting)"]
    end

    subgraph Edge["2. Edge & Fraud / AI Control Plane"]
        WAF["API Gateway & WAF"]
        VOP["Verification of Payee (VoP)<br/>IBAN / Name Match"]
        FRAUD["Real-Time Fraud & AML Engine<br/>(EU AI Act Governed + Human Override)"]
    end

    subgraph Core["3. Core Payment & Card Rails"]
        LEDGER["Core Payment Ledger<br/>(Critical ICT Function)"]
        SAFE["Safeguarding Accounts<br/>(Tier-1 Irish/EU Credit Institutions)"]
        SEPA["SEPA / SEPA Instant Clearing"]
        VAULT["PCI-DSS v4.0 Token Vault & HSM<br/>(CDE Isolated)"]
        SCHEME["Visa / Mastercard Networks"]
    end

    subgraph Gov["4. 2nd Line Assurance & CBI Reporting"]
        DORA["DORA Telemetry & RoI<br/>(4hr CBI Incident Clock)"]
        BOARD["Board Risk Committee & PCF Oversight"]
    end

    APP & API --> WAF --> VOP --> FRAUD
    FRAUD -->|Approved A2A| LEDGER
    LEDGER <--> SAFE
    LEDGER --> SEPA
    FRAUD -->|Approved Card| VAULT --> SCHEME
    LEDGER & VAULT & FRAUD -.->|Continuous KRIs & Logs| DORA --> BOARD
