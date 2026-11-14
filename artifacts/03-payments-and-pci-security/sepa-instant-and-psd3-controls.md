---
title: SEPA Instant, Verification of Payee & Safeguarding Controls
---

# SEPA Instant, PSD3/PSR & Safeguarding ICT Control Framework
**Entity Profile:** Irish-Authorised Payment Institution (PI/EMI)  
**Owners:** Head of ICT & InfoSec Risk (2nd Line) & PCF-56 Head of Safeguarding Oversight  
**Regulatory Basis:** EU Instant Payments Regulation (IPR), PSD2 → PSD3 / Payment Services Regulation (PSR), & Central Bank of Ireland (CBI) Safeguarding Requirements  

---

## 1. Regulatory Transition & Supervisory Context (Ireland)
Following the 2026 compromise texts and Official Journal publication of **PSD3** and the **Payment Services Regulation (PSR)**, Payment Institutions and Electronic Money Institutions are consolidated under a unified licensing regime with strict statutory transition windows:
* **T + 21 Months (General Application & Transposition):** PSR conduct, fraud-prevention, and Strong Customer Authentication (SCA) rules apply directly across the EEA, alongside national transposition of PSD3.
* **T + 27 Months (Mandatory Re-Authorisation & Verification of Payee):** Deadline to submit full Title II re-authorisation evidence to the **Central Bank of Ireland (CBI)** to avoid service suspension, and full enforcement of mandatory **Verification of Payee (VoP)** liability rules across all credit transfers.
* **CBI Safeguarding Zero-Tolerance Standard:** Under CBI thematic inspection expectations and **PCF-56 (Head of Safeguarding Oversight)** governance, ICT systems must enforce daily (`D+1`) segregation of user funds, automated daily internal/external reconciliations, and multi-bank concentration limits—backed by an annual **ISAE 3000** reasonable assurance audit.

---

## 2. SEPA Instant & Verification of Payee (VoP) Security Workflow

SEPA Instant mandates end-to-end settlement within **10 seconds (24/7/365)** while requiring pre-execution **Verification of Payee (VoP)** IBAN/name matching and real-time fraud screening.

```mermaid
sequenceDiagram
    autonumber
    actor Payer as Customer (Mobile App)
    participant GW as API Gateway & mTLS Edge
    participant VOP as Verification of Payee (VoP) Engine
    participant FRAUD as Real-Time Fraud & Sanctions AI
    participant LEDGER as Core Ledger & Safeguarding Control
    participant SEPA as SEPA Instant Clearing Rail

    Payer->>GW: Initiate SEPA Instant Transfer (IBAN + Payee Name + Amount)
    GW->>VOP: Query Beneficiary PSP Directory (ISO 20022)
    VOP-->>Payer: Return Match Status (Match / Close Match / No Match)
    Note over Payer,VOP: Explicit liability warning displayed if "Close" or "No Match"
    Payer->>GW: Confirm & Complete Hardware-Backed SCA (Dynamic Linking)
    GW->>FRAUD: Sub-Second Scoring (<300ms) + Impersonation/APP Risk Check
    alt High Impersonation / Fraud Score
        FRAUD-->>Payer: Step-Up Friction / Cooling-Off Hold + Analyst Review
    else Approved Within Risk Appetite
        FRAUD->>LEDGER: Debit User Balance & Tag Safeguarding Segregation Delta
        LEDGER->>SEPA: Dispatch Signed ISO 20022 pacs.008 Message (<10s SLA)
        SEPA-->>Payer: Instant Settlement Confirmation
    end
