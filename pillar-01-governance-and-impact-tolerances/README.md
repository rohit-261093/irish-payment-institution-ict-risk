---
title: Pillar 1 — Operational Resilience Governance, CIBS & Impact Tolerances
---

# Pillar 1: Operational Resilience Governance, CIBS & Impact Tolerances
**Regulatory Basis:** DORA Chapter II (Articles 5–6) · Central Bank of Ireland (CBI) Cross-Industry Guidance on Operational Resilience (Guidelines 1–7) · CBI Individual Accountability Framework (`IAF / SEAR`) · CBI ICT Self-Assessment Tool (`ICT-SAT`)

---

## 1. Why Pillar 1 Works This Way (Plain-English Q&A)

### Why start with "Critical or Important Business Services" (`CIBS`) instead of an IT server list?
**Because regulators and customers care about disrupted payment outcomes, not individual servers.**
If a microservice crashes silently and traffic fails over with zero customer impact, that is an IT event. If SEPA Instant clearing stops for 40 minutes, merchants cannot settle funds and the firm breaches its regulatory obligations. Pillar 1 anchors the entire 6-pillar operating system to five Board-approved **Critical or Important Business Services (`CIBS-01` to `CIBS-05`)**, ensuring every technical control in Pillars 2–6 is prioritized by external customer harm.

### How do you decide whether an Impact Tolerance should be 30 minutes or 4 hours?
**We calibrate disruption by time-bucket harm across four dimensions—never guesswork.**
In [`pillar-01-board-governance-and-harm-calibration.xlsx`](pillar-01-board-governance-and-harm-calibration.xlsx), we model what happens at `15m`, `30m`, `2h`, `4h`, and `24h` across **Customer Harm**, **Financial/Liquidity Loss**, **Safeguarding Ledger Integrity**, and **Regulatory/Market Contagion**. The point where harm becomes intolerable sets our Board-approved Recovery Time Objective (`RTO`) and Recovery Point Objective (`RPO`).

### What happens when a business team genuinely cannot fix a gap on time?
**They must request a time-boxed Risk Exception that expires automatically at 90 days.**
Silent risk acceptance is banned. Any control gap or overdue SLA requires a documented compensating control and an explicit expiry date (`<= 90 days`). Nothing can roll over silently—extending an exception past 90 days requires formal **Board Risk Committee** sign-off.

---

## 2. End-to-End Operating Process & Hard Decision Gates

1. **Step 1 — External `CIBS` vs. Internal `CIF` Classification (`Annual & Product Launch`):**
   * 2nd Line ICT Risk and Business Line Owners classify customer-facing payment rails (`CIBS-01` SEPA Instant, `CIBS-02` Card Acquiring, `CIBS-03` Safeguarding Ledger, `CIBS-04` Client Onboarding/Portal, `CIBS-05` Merchant Working Capital) separately from internal supporting functions (`CIFs`) in [`pillar-01-cibs-impact-tolerances.xlsx`](pillar-01-cibs-impact-tolerances.xlsx).
   * **HARD GATE 1 (New Product / Rail Launch Gate):** No new payment rail or customer-facing product may launch into production until it is mapped to a `CIBS`, assigned an accountable `PCF` owner, and given a Board-approved `RTO/RPO`.
2. **Step 2 — End-to-End Dependency Mapping (`Quarterly Refresh`):**
   * Engineering maps every `CIBS` down to its supporting applications, AWS Availability Zones (`eu-west-1`), Cloud HSM clusters, clearing schemes, and critical third-party APIs (`Dependency_Mapping` tab).
   * **HARD GATE 2 (Single-Point-of-Failure Gate):** Any `CIBS` dependency lacking active-active redundancy or a tested failover path is automatically flagged as a formal Risk Exception requiring remediation or Board waiver.
3. **Step 3 — Time-Bucket Harm Calibration & Board Approval (`Annual`):**
   * 2nd Line Risk runs workshops with Treasury, Safeguarding (`PCF-56`), and Operations to calibrate disruption harm across `15m–24h` buckets (`Time_Bucket_Harm_Matrix` tab) and submits `RTO/RPO` tolerances to the Board Risk Committee.
4. **Step 4 — `IAF/SEAR` Attestations, `ICT-SAT` & 90-Day Risk Exception Governance (`Quarterly`):**
   * Pre-Approval Controlled Function (`PCF`) holders complete quarterly "Reasonable Steps" attestations, and 2nd Line Risk completes the annual **CBI `ICT-SAT`** maturity self-assessment (`Board_Governance_And_Training` tab).
   * **HARD GATE 3 (90-Day Risk Exception Expiry Gate):** Any risk exception in `Risk_Exceptions_Register` reaching `90 days` without closure is automatically flagged `EXPIRED - BOARD ESCALATION` and escalated to the next Board Risk Committee meeting.

---

## 3. RACI & Accountability Matrix (`IAF / SEAR`)

| Pillar 1 Governance Activity | Board Risk Committee | CEO (`PCF-1`) & CRO (`PCF-14`) | Safeguarding (`PCF-56`) & MLRO (`PCF-52`) | CTO (`PCF-46`) & Engineering | Head of ICT & InfoSec Risk (2nd Line) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Annual `CIBS` & Impact Tolerance (`RTO/RPO`) Approval** | **A** | **C** | **C** | **C** | **R** |
| **End-to-End Dependency Mapping (`Apps / Cloud / Vendors`)** | **I** | **I** | **C** | **R** | **A (Challenge)** |
| **Time-Bucket Harm Calibration & `ICT-SAT` Submission** | **A** | **C** | **C** | **C** | **R** |
| **Risk Exception Approval (`<= 90 Days`)** | **I** | **A (`PCF-14`)** | **C** | **C (Control Plan)** | **R (Review)** |
| **Risk Exception Renewal (`> 90 Days`)** | **A** | **C** | **I** | **C** | **R (Escalation)** |

*(**R** = Responsible, **A** = Accountable, **C** = Consulted, **I** = Informed)*

---

## 4. Target Pillar 1 KPIs

| Metric / Outcome | Target Benchmark | Workbook & Formula Verification |
| :--- | :--- | :--- |
| **`CIBS` Impact Tolerance Compliance** | `0` live disruptions breaching Board-approved `RTO` or `RPO` | `Impact_Tolerances` & `Executive_Dashboard` |
| **Dependency Mapping Completeness** | `100%` of `CIBS-01`–`CIBS-05` mapped end-to-end (tech, cloud, vendors) | `Dependency_Mapping` tab |
| **Expired Risk Exceptions** | `0` risk exceptions open `> 90 days` without Board Risk Committee renewal | `Exception Status` in `Risk_Exceptions_Register` |
| **Board & Staff DORA / AI Literacy Training** | `100%` annual completion across Board `INEDs`, `PCFs`, and staff | `Board_Governance_And_Training` tab |

---

## 5. Supporting Excel Registers
1. **[`pillar-01-cibs-impact-tolerances.xlsx`](pillar-01-cibs-impact-tolerances.xlsx)** — `Executive_Dashboard` · `CIBS_and_CIF_Inventory` · `Dependency_Mapping` · `Impact_Tolerances`
2. **[`pillar-01-board-governance-and-harm-calibration.xlsx`](pillar-01-board-governance-and-harm-calibration.xlsx)** — `Governance_Dashboard` · `Time_Bucket_Harm_Matrix` · `Board_Governance_And_Training` · `Risk_Exceptions_Register`
