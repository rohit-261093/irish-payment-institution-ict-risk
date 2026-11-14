---
title: Irish Regulated Payment Institution — Head of Security & ICT Risk Playbook
---

# Irish Regulated Payment Institution (PI/EMI)
### Practical Security Leadership, Operational Resilience & AI Governance Playbook

An operator's blueprint for running **Information Security, ICT Risk, and Regulatory Compliance** inside a **Central Bank of Ireland (CBI)–authorised Payment Institution**, designed from the perspective of a **Head of Security / ICT & InfoSec Risk reporting directly to the CTO**.

Rather than theoretical frameworks or bloated policy manuals, this repository contains the **day-to-day leadership artefacts** used to keep payment rails resilient, unblock product and engineering teams, and maintain continuous readiness for Central Bank of Ireland supervisory reviews across **DORA**, **PSD2/PSD3**, **PCI-DSS v4.0**, and the **EU AI Act**.

---

## 1. Operating Philosophy: Security as a Commercial Enabler
In a lean, fast-moving Irish fintech, security cannot function as a department of "no." Every playbook in this repository follows four practical rules:
* **Protect the Crown Jewels First:** Concentrate engineering effort on what can actually sink a Payment Institution—**SEPA Instant availability**, **cardholder data (CDE) isolation**, and **daily `D+1` safeguarding of customer funds**.
* **Fast-Track Low-Risk Work, Gate High-Risk Work:** Give product teams self-service guardrails for routine changes while enforcing hard stops on unvetted third-party data sharing, high-risk AI models, and safeguarding ledger changes.
* **No Silent Risk Deferrals:** Engineering can defer a non-critical patch for business reasons, but every exception requires a compensating control, a hard expiry date (`<= 90 days`), and explicit sign-off.
* **Always Audit-Ready for the CBI:** Evidence for DORA, safeguarding (`ISAE 3000`), and ICT inspections is generated as a by-product of normal operations—not assembled in a panic two weeks before a regulatory visit.

---

## 2. Core Leadership Playbooks (Repository Guide)

| Playbook | Purpose & Audience | What It Solves on Monday Morning |
| :--- | :--- | :--- |
| **[01. 30-60-90 Day Head of Security Execution Plan](playbooks/01-30-60-90-day-execution-plan.md)** | **CTO, CEO & Board** | Maps exact priorities across Months 1–3: auditing DORA RoI and safeguarding controls, clearing quick-win engineering bottlenecks, and running an executive incident tabletop. |
| **[02. 1-Page Board & CTO Risk Report](playbooks/02-board-and-cto-risk-report.md)** | **Board Risk Committee & Executive Team** | Replaces 40-page technical slide decks with a single executive view of RAG posture, top ICT risks, patch SLA trends, and formal risk acceptance sign-offs. |
| **[03. "2 AM" Incident & CBI Reporting Playbook](playbooks/03-2am-incident-and-cbi-reporting-playbook.md)** | **On-Call Engineering, Ops & Legal** | Step-by-step crisis checklist for a SEPA outage, vendor breach, or safeguarding break—defining who joins the call, DORA severity thresholds, and the **4-hour CBI notification clock**. |
| **[04. Fast-Track Vendor & AI Review Checklist](playbooks/04-fast-track-vendor-and-ai-review.md)** | **Product, Procurement & Engineering** | Lightweight intake gate for onboarding SaaS tools and vetting AI features—separating **EU AI Act Art. 50** chatbots from **Annex III** credit scoring and enforcing **DORA Art. 30** clauses. |
| **[05. CBI Supervisory Inspection Readiness Binder](playbooks/05-cbi-supervisory-readiness-binder.md)** | **CBI Supervisors & External Auditors** | Master evidence index covering the DORA Register of Information, signed bank safeguarding letters, disaster recovery test results, and pen-test closure logs. |

---

## 3. Irish & EU Regulatory Scope (What Matters in Practice)

| Regulation | Irish Supervisory Reality | Practical Control Ownership |
| :--- | :--- | :--- |
| **DORA & CBI Operational Resilience** | Active supervision via **CBI Portal** annual Register of Information (RoI) submissions, **ICT-SAT** returns, 4-hour major incident reporting, and **TIBER-IE** testing. | Maintain a clean vendor/LEI register, test failover recovery against Board impact tolerances, and run deterministic incident triage. |
| **PSD2 → PSD3 / PSR & Safeguarding** | Zero CBI tolerance for safeguarding breaks (`D+1` segregation, daily reconciliations, multi-bank concentration) alongside **Verification of Payee (VoP)** and APP fraud controls. | Enforce database controls preventing negative balance netting, automate daily `camt.053` matching, and log all VoP/SCA outcomes. |
| **EU AI Act & Irish AI Act 2026** | Supervised in financial services by the **Central Bank of Ireland**; **Art. 4** (AI literacy) and **Art. 50** (chatbot transparency) are live now, with **Annex III** high-risk rules due Dec 2027. | Keep a single AI register distinguishing **Annex III high-risk credit scoring** from **excluded fraud-detection models**, with strict PII/PAN redaction on external LLMs. |
| **PCI-DSS v4.0** | Strict focus on Cardholder Data Environment (CDE) scope reduction, HSM key management, and payment page script integrity (`Req. 6.4.3` & `11.6.1`). | Keep raw PANs isolated inside a third-party tokenization vault so core microservices remain out of CDE scope. |
| **CBI Individual Accountability (IAF)** | Clear accountability across Pre-Approval Controlled Functions—including **CEO (PCF-1)**, **Board Risk Chair (PCF-5)**, **MLRO (PCF-52)**, and **Head of Safeguarding (PCF-56)**. | Tie every risk exception, safeguarding break, and critical vendor relationship to a named executive owner. |

---

## 4. Supporting Operational Trackers (`.xlsx`)
Alongside the narrative playbooks above, the [`trackers/`](trackers/) folder contains ready-to-use Excel registers with built-in formulas, RAG conditional formatting, and executive summary charts:
* [`cibs-impact-tolerances.xlsx`](trackers/cibs-impact-tolerances.xlsx) — Business service impact tolerances (`RTO/RPO`) and 90-day risk exception tracker.
* [`ict-asset-vuln-sla-tracker.xlsx`](trackers/ict-asset-vuln-sla-tracker.xlsx) — CVSS/KEV vulnerability SLA calculator and pre-release change gate log.
* [`dora-incident-cbi-clock.xlsx`](trackers/dora-incident-cbi-clock.xlsx) — DORA major incident threshold calculator generating exact `4h` and `72h` CBI deadlines.
* [`resilience-testing-tiber-ie.xlsx`](trackers/resilience-testing-tiber-ie.xlsx) — BCDR failover scorecard and TIBER-IE red-team remediation tracker.
* [`dora-roi-and-vendor-exit.xlsx`](trackers/dora-roi-and-vendor-exit.xlsx) — EBA DPM 4.0 vendor register with 20-character LEI validation and exit drill schedule.
* [`safeguarding-psd3-ai-register.xlsx`](trackers/safeguarding-psd3-ai-register.xlsx) — Daily `D+1` safeguarding reconciliation log and EU AI Act system inventory.

---

## 5. Industry Reference Benchmarks
* **Supervisory Standards:** Central Bank of Ireland **ICT Self-Assessment Tool (ICT-SAT)**, **TIBER-IE** Framework, **EBA DORA Register of Information (DPM 4.0)**, and Ireland's **Regulation of Artificial Intelligence Act 2026**.
* **Community AI Governance Reference:** [Taimur Ijlal — AI Governance Repository](https://github.com/taimurijlal/AIGovernance) *(Referenced for general AI policy checklists and ISO/IEC 42001 structure).*
