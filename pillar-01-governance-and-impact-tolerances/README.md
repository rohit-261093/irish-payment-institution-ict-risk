---
title: Pillar 1 — Resilience Governance, Business Service Mapping & Impact Tolerances
---

# Pillar 1: Resilience Governance, Business Service Mapping & Impact Tolerances
**Regulatory Basis:** DORA Chapter II (Articles 5–6) · Central Bank of Ireland (CBI) Cross-Industry Guidance on Operational Resilience · CBI Individual Accountability Framework (IAF / SEAR)

---

## 1. Core Governance Rules
1. **External CIBS vs. Internal CIFs:** Under CBI Operational Resilience Guidance, **Critical or Important Business Services (CIBS)** are strictly *external-facing* services delivered to customers or merchants (such as SEPA Instant transfers or card authorization). Internal systems and vendors supporting those services (such as the Core Ledger, Cloud HSM, or AWS hosting) are mapped as **Critical or Important Functions (CIFs)** under DORA.
2. **Risk Appetite vs. Impact Tolerance:** **Risk Appetite** is the internal amber early-warning threshold where engineering and 2nd Line intervene. **Impact Tolerance** is the hard red ceiling (RTO/RPO) beyond which disruption causes intolerable harm to customers, the firm's safeguarding obligations, or market integrity.
3. **No Silent Risk Deferrals:** Engineering cannot defer resilience or security fixes informally. Every exception requires documented compensating controls, a hard expiry date (`<= 90 calendar days`), and formal sign-off from the **Head of ICT & InfoSec Risk** and accountable **PCF**.

---

## 2. End-to-End Operating Process & Decision Gates

1. **Step 1 — Service Classification (New Product / Annual Review):**
   * Product and 2nd Line ICT Risk classify every customer-facing capability to determine whether disruption would cause intolerable customer or financial harm, assigning a `CIBS` ID.
   * **Hard Gate:** No new payment rail, card product, or customer API goes live in production without an approved CIBS mapping and assigned PCF owner.
2. **Step 2 — End-to-End Dependency Mapping:**
   * Engineering maps every person, core application, cloud availability zone, third-party vendor, and fourth-party subcontractor required to deliver each CIBS inside **`CIBS_Dependency_Matrix`**.
   * **Hard Gate:** Any single point of failure (SPOF) across cloud regions, HSM clusters, or safeguarding banks triggers a mandatory remediation plan or formal Risk Exception.
3. **Step 3 — Board Impact Tolerance & Risk Appetite Calibration:**
   * The Head of ICT Risk proposes amber **Risk Appetite** warning triggers and hard red **Impact Tolerances (RTO/RPO)** for annual approval by the **Board Risk Committee**.
4. **Step 4 — Exception Governance & Annual CBI Self-Assessment:**
   * Temporary control gaps are logged in **`Risk_Exception_Register`** with a mandatory 90-day expiry. Any expired exception automatically escalates to the Board Risk Committee.
   * Annually, empirical failover results and exception trends feed into the Board-approved **CBI Operational Resilience Self-Assessment**.

---

## 3. RACI & CBI PCF Accountability Matrix

| Governance Activity | Board Risk Committee (PCF-3/5) | CEO (PCF-1/8) | CTO (1st Line Tech) | Head of ICT Risk (2nd Line) | Head of Safeguarding (PCF-56) | MLRO (PCF-52) |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **CIBS Identification & Impact Tolerance Approval** | **A** | **R** | **C** | **R** | **C** | **C** |
| **System, Cloud & Vendor Dependency Mapping** | **I** | **I** | **R** | **A / Challenge** | **C** | **C** |
| **Safeguarding Ledger Tolerance & Sweep SLAs** | **I** | **A** | **R** | **C** | **R** | **I** |
| **Risk Exception Sign-Off (Low / Medium Residual)** | **I** | **I** | **R** | **A** | **C** | **C** |
| **Risk Exception Sign-Off (High Residual Risk)** | **A** | **C** | **R** | **R** | **C** | **C** |
| **Annual CBI OpRes Self-Assessment & DORA Art. 5 Sign-Off** | **A** | **R** | **C** | **R** | **C** | **C** |

*(**R** = Responsible, **A** = Accountable, **C** = Consulted, **I** = Informed)*

---

## 4. Target Governance Outcomes & KPIs

| Metric / Outcome | Target Benchmark | How It Is Measured |
| :--- | :--- | :--- |
| **CIBS Dependency Coverage** | `100%` of external payment & safeguarding services mapped | Annual Board sign-off on `CIBS_Dependency_Matrix` |
| **Failover Recovery Margin** | Actual test recovery `<= 75%` of Board Impact Tolerance | `Tolerance Margin (Mins)` column in `CIBS_Dependency_Matrix` |
| **Risk Exception Discipline** | `0` expired exceptions without Board Risk Committee escalation | `Governance Status` formula in `Risk_Exception_Register` |
| **Supervisory Readiness** | `100%` on-time annual **CBI Operational Resilience Self-Assessment** | Board Risk Committee minutes & submission log |

---

## 5. Supporting Excel Register
All live service mappings, tolerance thresholds, and active 90-day exceptions are maintained in **[`pillar-01-cibs-impact-tolerances.xlsx`](pillar-01-cibs-impact-tolerances.xlsx)** across three tabs:
* **`Executive_Summary`:** KPI summary cards and Tolerance vs. Actual Failover chart.
* **`CIBS_Dependency_Matrix`:** Master mapping of external business services, DORA CIFs, cloud regions, PCF owners, and RTO/RPO limits.
* **`Risk_Exception_Register`:** 90-day exception log with automatic expiry countdowns and RAG status alerts.
