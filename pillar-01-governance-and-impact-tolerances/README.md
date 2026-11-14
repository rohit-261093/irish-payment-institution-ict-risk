---
title: Pillar 1 — Resilience Governance, Business Service Mapping & Impact Tolerances
---

# Pillar 1: Resilience Governance, Business Service Mapping & Impact Tolerances
**Regulatory Basis:** DORA Chapter II (Articles 5–6) · Central Bank of Ireland (CBI) Cross-Industry Guidance on Operational Resilience · CBI Individual Accountability Framework (IAF / SEAR)

---

## 1. Core Governance Rules
1. **External CIBS vs. Internal CIFs:** Under CBI Operational Resilience Guidance, **Critical or Important Business Services (CIBS)** are strictly *external-facing* services delivered to customers or merchants (such as SEPA Instant transfers or card authorization). Internal systems and vendors supporting those services (such as the Core Ledger, Cloud HSM, or AWS hosting) are mapped as **Critical or Important Functions (CIFs)** under DORA.
2. **Evidence-Based Harm Calibration:** Every Board-approved Impact Tolerance (`RTO/RPO`) must be backed by a documented time-bucket harm assessment across **Customer Harm**, **Safeguarding & Liquidity Harm**, and **Regulatory / Market Integrity Harm**—proving the exact point at which disruption becomes intolerable.
3. **Board Article 5 & IAF Accountability:** Under DORA Article 5 and the CBI Individual Accountability Framework, the Board formally approves the ICT Risk Framework, ICT security budget/headcount adequacy, and annual Operational Resilience Self-Assessment, supported by mandatory annual DORA/AI training and quarterly PCF attestations.
4. **No Silent Risk Deferrals:** Engineering cannot defer resilience or security fixes informally. Every exception requires documented compensating controls, a hard expiry date (`<= 90 calendar days`), and formal sign-off from the **Head of ICT & InfoSec Risk** and accountable **PCF**.

---

## 2. End-to-End Operating Process & Decision Gates

1. **Step 1 — Service Classification (New Product / Annual Review):**
   * Product and 2nd Line ICT Risk classify every customer-facing capability to determine whether disruption would cause intolerable customer or financial harm, assigning a `CIBS` ID.
   * **Hard Gate:** No new payment rail, card product, or customer API goes live in production without an approved CIBS mapping and assigned PCF owner.
2. **Step 2 — End-to-End Dependency Mapping:**
   * Engineering maps every person, core application, cloud availability zone, third-party vendor, and fourth-party subcontractor required to deliver each CIBS inside **`CIBS_Dependency_Matrix`**.
   * **Hard Gate:** Any single point of failure (SPOF) across cloud regions, HSM clusters, or safeguarding banks triggers a mandatory remediation plan or formal Risk Exception.
3. **Step 3 — Time-Bucket Harm Calibration & Tolerance Approval:**
   * 2nd Line ICT Risk and PCF owners score disruption impact across `15m`, `30m`, `1h`, `4h`, and `24h` intervals in **`Impact_Harm_Calibration`** to establish amber **Risk Appetite** triggers and hard red **Impact Tolerances (RTO/RPO)** for Board Risk Committee approval.
4. **Step 4 — Exception Governance, IAF Attestations & Annual CBI Self-Assessment:**
   * Temporary control gaps are logged in **`Risk_Exception_Register`** with a mandatory 90-day expiry. Any expired exception automatically escalates to the Board Risk Committee.
   * Quarterly PCF attestations, annual Board DORA/AI training (`PCF_IAF_And_Board_Training`), and empirical failover results feed into the Board-approved **`CBI_OpRes_Self_Assessment`**.

---

## 3. RACI & CBI PCF Accountability Matrix

| Governance Activity | Board Risk Committee (PCF-3/5) | CEO (PCF-1/8) | CTO (1st Line Tech) | Head of ICT Risk (2nd Line) | Head of Safeguarding (PCF-56) | MLRO (PCF-52) |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **CIBS Identification, Harm Calibration & Tolerance Approval** | **A** | **R** | **C** | **R** | **C** | **C** |
| **System, Cloud & Vendor Dependency Mapping** | **I** | **I** | **R** | **A / Challenge** | **C** | **C** |
| **ICT Security Budget & Headcount Adequacy (DORA Art. 5)** | **A** | **R** | **R** | **C** | **I** | **I** |
| **Safeguarding Ledger Tolerance & Sweep SLAs** | **I** | **A** | **R** | **C** | **R** | **I** |
| **Risk Exception Sign-Off (Low / Medium Residual)** | **I** | **I** | **R** | **A** | **C** | **C** |
| **Risk Exception Sign-Off (High Residual Risk)** | **A** | **C** | **R** | **R** | **C** | **C** |
| **Annual CBI OpRes Self-Assessment & Quarterly IAF Attestations** | **A** | **R** | **R** | **R** | **R** | **R** |

*(**R** = Responsible, **A** = Accountable, **C** = Consulted, **I** = Informed)*

---

## 4. Target Governance Outcomes & KPIs

| Metric / Outcome | Target Benchmark | How It Is Measured |
| :--- | :--- | :--- |
| **CIBS Dependency & Harm Justification** | `100%` of external business services mapped & time-bucket calibrated | `CIBS_Dependency_Matrix` & `Impact_Harm_Calibration` tabs |
| **Failover Recovery Margin** | Actual test recovery `<= 75%` of Board Impact Tolerance | `Tolerance Margin (Mins)` column in `CIBS_Dependency_Matrix` |
| **Risk Exception Discipline** | `0` expired exceptions without Board Risk Committee escalation | `Governance Status` formula in `Risk_Exception_Register` |
| **Board & PCF Accountability** | `100%` annual DORA/AI training & quarterly IAF attestations on time | `PCF_IAF_And_Board_Training` compliance status |
| **Supervisory Readiness** | `100%` on-time annual **CBI Operational Resilience Self-Assessment** | `CBI_OpRes_Self_Assessment` maturity tracker & Board minutes |

---

## 5. Supporting Excel Registers
All live service mappings, harm calibrations, Board self-assessments, and active 90-day exceptions are maintained across two companion Excel workbooks in this folder:

1. **[`pillar-01-cibs-impact-tolerances.xlsx`](pillar-01-cibs-impact-tolerances.xlsx)**
   * **`Executive_Summary`:** KPI summary cards and Tolerance vs. Actual Failover chart.
   * **`CIBS_Dependency_Matrix`:** Master mapping of external business services, DORA CIFs, cloud regions, PCF owners, and RTO/RPO limits.
   * **`Risk_Exception_Register`:** 90-day exception log with automatic expiry countdowns and RAG status alerts.
2. **[`pillar-01-board-governance-and-harm-calibration.xlsx`](pillar-01-board-governance-and-harm-calibration.xlsx)**
   * **`Board_Governance_Dashboard`:** Executive maturity KPIs, training/attestation completion rates, and maturity chart.
   * **`Impact_Harm_Calibration`:** Time-bucket harm scoring (`15m` to `24h`) justifying Board RTO thresholds.
   * **`CBI_OpRes_Self_Assessment`:** Annual CBI Operational Resilience & DORA Article 5 maturity assessment.
   * **`PCF_IAF_And_Board_Training`:** Annual DORA/AI training and quarterly CBI IAF/SEAR attestation log.
