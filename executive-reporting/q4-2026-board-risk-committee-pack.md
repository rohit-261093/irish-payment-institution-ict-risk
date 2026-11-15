---
title: Q4 2026 Board Risk Committee Report — ICT Risk, Operational Resilience & AI Governance
---

# Board Risk Committee Report — Q4 2026
**Prepared By:** Head of ICT & InfoSec Risk (2nd Line) · **Submitted To:** Board Risk Committee (`INEDs`) · **Data Cutoff:** November 2026 · **Companion Scorecard:** [`board-ict-risk-and-resilience-scorecard.xlsx`](board-ict-risk-and-resilience-scorecard.xlsx)

---

## 1. Executive Posture Summary: **GREEN (Within Board Risk Appetite)**

During Q4 2026, all **10 Enterprise Key Risk Indicators (`KRI-01` to `KRI-10`)** operated within Board-approved Risk Appetite thresholds across our five Critical or Important Business Services (`CIBS-01` to `CIBS-05`):
* **Zero Impact Tolerance Breaches (`Pillar 1`):** SEPA Instant (`CIBS-01`, `30-min` RTO) and Card Acquiring (`CIBS-02`, `45-min` RTO) experienced zero availability breaches. All prior `90-day` risk exceptions have been remediated and closed (`0` expired exceptions).
* **Accelerated Vulnerability & Change Hygiene (`Pillar 2`):** Critical (`CVSS >= 9.0`) and CISA KEV remediation reached **98.5%** within the `7-day` SLA (up from `94.0%` in Q3), and `100%` of privileged entitlements across Cloud HSMs, AWS root accounts, and depositary banking portals completed quarterly PAM recertification.
* **Regulatory Incident Readiness (`Pillar 3`):** Mean Time to Classify (`MTTC`) averaged **28 minutes** against our `45-minute` hard gate, maintaining **100%** on-time performance for the Central Bank of Ireland (`CBI`) 4-hour reporting clock. Four scenario-specific Incident Response Playbooks (`IRP-01` to `IRP-04`, including an enterprise Microsoft 365/Outlook disruption playbook) are now active.
* **Empirical Resilience & TIBER-IE Closure (`Pillar 4`):** Q3/Q4 BCDR active-active failover drills restored `CIBS-01` in **18 minutes** (`60%` of the `30-minute` Impact Tolerance). All Critical and High findings from the TIBER-IE threat-led penetration test were remediated and verified via Purple-Team replay inside the `60-day` SLA.
* **DORA Register of Information & Stressed Exits (`Pillar 5`):** The EBA DPM 4.0 Register of Information passed pre-submission XBRL validation (`100%` valid 20-character LEIs) ahead of the annual CBI Portal filing. Annual stressed exit tabletop drills were completed for AWS (`eu-west-1`) and ClearBank.
* **EU AI Act & Irish AI Act 2026 Deployer Assurance (`Pillar 6`):** Following commencement of Ireland's *Regulation of Artificial Intelligence Act 2026*, the firm maintains **zero in-house trained models** (`100%` third-party AI Deployer posture). Signed `Article 27` FRIAs are active for `AI-002` (Merchant Underwriting) and `AI-004` (Biometric eKYC), quarterly vendor bias/conformity audit packs are `100%` current, and Zscaler CASB blocked `4` unsanctioned Shadow AI tools at the network proxy.

---

## 2. Key Risk Indicators (KRIs) & Trend Highlights

| KRI ID | Metric | Risk Appetite | Q3 Actual | Q4 Current | Status |
| :--- | :--- | :---: | :---: | :---: | :---: |
| `KRI-01` | Live `CIBS` Impact Tolerance Breaches (`> RTO`) | `0` | `0` | `0` | **WITHIN APPETITE** |
| `KRI-02` | Expired Risk Exceptions (`> 90 Days`) | `0` | `1` | `0` | **WITHIN APPETITE** |
| `KRI-03` | Critical / CISA KEV Vulnerabilities Patched `<= 7d` | `>= 95.0%` | `94.0%` | `98.5%` | **WITHIN APPETITE** |
| `KRI-04` | Quarterly PAM Recertification Completion | `100.0%` | `100.0%` | `100.0%` | **WITHIN APPETITE** |
| `KRI-05` | On-Time CBI `4h` / `72h` Incident Filings | `100.0%` | `100.0%` | `100.0%` | **WITHIN APPETITE** |
| `KRI-06` | TIBER-IE & Critical/High Pen-Test Findings Closed `<= 60d` | `100.0%` | `90.0%` | `100.0%` | **WITHIN APPETITE** |
| `KRI-07` | `CIF`-Critical Vendors Exit-Drilled (`<= 365d`) | `100.0%` | `85.0%` | `100.0%` | **WITHIN APPETITE** |
| `KRI-08` | DORA RoI Validated 20-Character LEI Accuracy | `100.0%` | `100.0%` | `100.0%` | **WITHIN APPETITE** |
| `KRI-09` | High-Risk `Annex III` AI APIs With Signed `Art. 27` FRIA | `100.0%` | `100.0%` | `100.0%` | **WITHIN APPETITE** |
| `KRI-10` | Unsanctioned Shadow AI Tools Blocked at Egress Proxy | `100.0%` | `100.0%` | `100.0%` | **WITHIN APPETITE** |

---

## 3. Emerging Risks & Management Actions Underway

1. **Hyperscaler & Enterprise Productivity Concentration (`Pillar 3` & `Pillar 5`):**
   * *Observation:* Recent industry-wide Microsoft 365 / Exchange Online disruptions highlight the risk of staff relying on email as an informal intake channel for client payment instructions or treasury approvals.
   * *Management Action (`BRC-2026-05`):* `IRP-03` is now operational with a strict anti-BEC/Shadow-IT freeze, and Payments Operations is migrating all remaining manual email payment instructions onto the MFA-authenticated Client Portal by **18 December 2026**.
2. **Third-Party AI Vendor Model Drift (`Pillar 6`):**
   * *Observation:* Continuous vendor updates to `AI-001` (Fraud Scoring) and `AI-004` (Biometric Liveness) require disciplined post-update validation.
   * *Management Action:* Mandatory quarterly vendor bias/conformity audit pack reviews and `60-second` API feature-flag kill-switches remain enforced across all production AI endpoints.

---

## 4. Matters Requested for Board Risk Committee Approval

1. **Approve** the annual **CIBS Impact Tolerance & Harm Calibration Matrix** (`Pillar 1`) retaining the `30-minute` SEPA Instant and `45-minute` Card Acquiring tolerances.
2. **Note** the `100%` closure and Purple-Team replay verification of Q3 **TIBER-IE** findings (`Pillar 4`).
3. **Authorise** submission of the validated **EBA DPM 4.0 DORA Register of Information (`XBRL`)** to the Central Bank of Ireland Portal (`Pillar 5`).
4. **Note** quarterly `IAF/SEAR` "Reasonable Steps" control attestations completed by `PCF-1`, `PCF-14`, `PCF-46`, `PCF-52`, and `PCF-56`.
