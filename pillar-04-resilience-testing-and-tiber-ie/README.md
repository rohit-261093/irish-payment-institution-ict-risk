---
title: Pillar 4 — Digital Operational Resilience Testing & TIBER-IE TLPT
---

# Pillar 4: Digital Operational Resilience Testing & TIBER-IE TLPT
**Regulatory Basis:** DORA Chapter IV (Articles 24–27) · Central Bank of Ireland (CBI) Cross-Industry Guidance on Operational Resilience (*Respond & Recover*, Guidelines 8–9) · TIBER-IE Framework · PCI-DSS v4.0 Requirement 11.4

---

## 1. What Pillar 4 Means in Practice
In Pillars 1–3, the Payment Institution establishes Board-approved Impact Tolerances (`30 mins` for SEPA Instant, `45 mins` for card authorization), hardens underlying systems, and enforces a 4-hour CBI incident reporting clock. **Pillar 4 proves empirically that those controls hold up under live stress.**

During Central Bank of Ireland operational resilience inspections, supervisors look past paper Business Continuity plans and test three operational realities:
1. **Empirical Validation Against Impact Tolerances (`CBI Guideline 8` & `DORA Art. 25`):** Severe-but-plausible disruption scenarios (such as an AWS `eu-west-1` availability zone failure during peak payroll clearing or a depositary bank ISO 20022 feed outage) must be tested live, with actual failover recovery staying safely within Board Impact Tolerances (`<= 75%` utilization target).
2. **Full DORA Article 25 & PCI-DSS v4.0 Test Breadth:** Beyond BCDR failover, the annual test programme covers source code security reviews, performance/capacity stress tests, physical data centre inspections, and **PCI-DSS v4.0** 6-monthly Cardholder Data Environment (CDE) segmentation pen-tests.
3. **Threat-Led Penetration Testing (`TIBER-IE` / `DORA Art. 26–27`):** Intelligence-led red-team exercises aligned to **TIBER-IE** test live payment rails against realistic threat actors—backed by strict **Article 27** tester independence vetting, **MITRE ATT&CK** mapping, a **60-day remediation SLA**, and mandatory **Purple-Team replay** before any critical or high finding is closed.

---

## 2. Regulatory Alignment Matrix (DORA, CBI, TIBER-IE & PCI-DSS)

| Regulatory Anchor | Specific Supervisory Requirement | How Pillar 4 Operationalises It |
| :--- | :--- | :--- |
| **DORA Art. 24–25** & **CBI OpRes Guideline 9** | Establish a risk-based annual digital operational resilience testing programme covering BCDR, load/stress, source code, network, and physical security. | **`Annual_DORA_Test_Programme`:** Schedules and tracks all mandatory test categories mapped directly to `CIBS-01`–`CIBS-05`. |
| **CBI OpRes Guideline 8** & **DORA Art. 25(1)** | Test severe-but-plausible scenarios to prove the firm can remain within Board Impact Tolerances during operational disruption. | **`BCDR_Scenario_Scorecard`:** Measures actual recovery minutes against Board RTOs and flags drills exceeding the `75%` utilization buffer. |
| **PCI-DSS v4.0 Req. 11.4.5** | Perform network segmentation penetration testing at least every 6 months to confirm CDE isolation. | **`Annual_DORA_Test_Programme` & `TIBER_IE_And_Pentest_Findings`:** Enforces semi-annual QSA segmentation testing on `CIBS-02` CDE enclaves. |
| **DORA Art. 26** & **TIBER-IE Framework** | Conduct intelligence-led red-team testing on live production systems supporting critical functions, followed by purple-team replay. | **`TIBER_IE_And_Pentest_Findings`:** Maps findings to **MITRE ATT&CK**, enforces a `60-day` fix SLA, and requires Purple-Team replay prior to closure. |
| **DORA Art. 27** | Verify external/internal tester qualifications, conflict-of-interest independence, indemnity coverage, and risk management controls. | **`Tester_Independence_And_Scope`:** Pre-engagement vetting log confirming CREST/QSA certifications, independence, and 2nd Line sign-off. |

---

## 3. End-to-End Resilience Testing & TLPT Process

1. **Step 1 — Annual Risk-Based Test Planning (`Q1 Board Sign-Off`):**
   * Head of ICT & InfoSec Risk and CTO publish the annual schedule in **`Annual_DORA_Test_Programme`**, ensuring every `CIBS-01`–`CIBS-05` service undergoes BCDR failover, load stress, and security testing.
2. **Step 2 — Tester Vetting & Rules of Engagement Gate (`DORA Art. 27`):**
   * Before any external pen-test or TIBER-IE red-team engagement begins, 2nd Line ICT Risk logs tester credentials, independence checks, NDA/indemnity, and live production safety guardrails in **`Tester_Independence_And_Scope`**.
   * **Hard Gate:** No live production red-team or CDE segmentation test may start without signed Rules of Engagement and 2nd Line ICT Risk approval.
3. **Step 3 — Severe-But-Plausible Scenario & Failover Execution:**
   * Engineering executes quarterly/semi-annual failover drills (AZ loss, Cloud HSM quorum switch, depositary bank feed outage) and records actual recovery minutes in **`BCDR_Scenario_Scorecard`**.
   * **Hard Gate:** Any drill exceeding `100%` of the Board Impact Tolerance triggers a mandatory remediation action and an immediate Pillar 1 Risk Exception (`<= 90 days`).
4. **Step 4 — 60-Day Remediation & Purple-Team Replay Closure:**
   * All TIBER-IE and penetration test findings are logged in **`TIBER_IE_And_Pentest_Findings`** with a **60-calendar-day** remediation deadline.
   * **Hard Gate:** A finding cannot be marked `CLOSED - REPLAYED` based solely on a developer pull request—SecOps and the red team must execute a **Purple-Team replay** confirming the original exploit path is blocked.

---

## 4. RACI & Accountability Matrix

| Testing & TLPT Activity | Board Risk Committee (PCF-3/5) | CTO / 1st Line Engineering | SecOps / Purple Team | Head of ICT & InfoSec Risk (2nd Line) | External TIBER-IE / QSA Testers |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Annual DORA Test Programme Approval** | **A** | **C** | **C** | **R** | **I** |
| **DORA Art. 27 Tester Vetting & Scope Sign-Off** | **I** | **C** | **C** | **A / R** | **C** |
| **Quarterly BCDR & Failover Drill Execution** | **I** | **R** | **C** | **A (Challenge)** | **I** |
| **TIBER-IE Red Team & CDE Pen-Test Execution** | **I** | **I (Blind Test)** | **C (Blue Team)** | **A (Control Group)** | **R** |
| **60-Day Finding Remediation & Code Fixes** | **I** | **A / R** | **C** | **I / Escalation** | **I** |
| **Purple-Team Replay & Final Finding Closure** | **I** | **C** | **R** | **A (Sign-Off)** | **C** |

*(**R** = Responsible, **A** = Accountable, **C** = Consulted, **I** = Informed)*

---

## 5. Target Resilience Testing KPIs

| Metric / Outcome | Target Benchmark | How It Is Measured |
| :--- | :--- | :--- |
| **Annual Test Plan Execution** | `100%` of scheduled DORA Art. 25 & PCI tests completed on time | `Execution Status` in `Annual_DORA_Test_Programme` |
| **BCDR Impact Tolerance Margin** | Actual recovery `<= 75%` of Board Impact Tolerance (`0` breaches) | `Tolerance Utilization %` & `Assurance Verdict` in `BCDR_Scenario_Scorecard` |
| **TIBER-IE & Critical/High Closure SLA** | `100%` remediated and Purple-Team replayed within `60 days` | `Governance Status` in `TIBER_IE_And_Pentest_Findings` |
| **Tester Independence Compliance** | `100%` of external engagements vetted under DORA Art. 27 | `Tester_Independence_And_Scope` approval log |

---

## 6. Supporting Excel Registers
All annual test schedules, BCDR failover scorecards, TIBER-IE/pen-test findings, and DORA Article 27 tester vetting records are maintained across two companion Excel workbooks in this folder:

1. **[`pillar-04-resilience-testing-scorecard.xlsx`](pillar-04-resilience-testing-scorecard.xlsx)**
   * **`Testing_Assurance_Dashboard`:** Executive KPI cards and Board Tolerance vs. Actual Failover chart.
   * **`Annual_DORA_Test_Programme`:** Master schedule covering BCDR, CDE segmentation, load stress, source code, physical security, and TIBER-IE testing.
   * **`BCDR_Scenario_Scorecard`:** Empirical failover timing against Board RTOs with automated `75%` margin checks.
2. **[`pillar-04-pentest-and-tiber-ie-tracker.xlsx`](pillar-04-pentest-and-tiber-ie-tracker.xlsx)**
   * **`TLPT_And_Pentest_Dashboard`:** Finding closure KPIs and remediation status chart.
   * **`TIBER_IE_And_Pentest_Findings`:** MITRE ATT&CK finding tracker enforcing a 60-day SLA and mandatory Purple-Team replay verification.
   * **`Tester_Independence_And_Scope`:** DORA Article 27 qualification, conflict-of-interest, and scope approval register.
