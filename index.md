---
title: Irish Regulated Payment Institution (PI/EMI) — Digital Operational Resilience Blueprint
---

# Irish Regulated Payment Institution (PI/EMI)
### 6-Pillar Digital Operational Resilience, Payment Security & AI Governance Operating System

An executive reference architecture demonstrating how a **Central Bank of Ireland (CBI)–authorised Payment Institution** operationalises **DORA (Chapters II–VI)**, **CBI Cross-Industry Operational Resilience Guidance**, **PSD2/PSD3 re-authorisation**, **PCI-DSS v4.0**, and the **EU AI Act / Regulation of Artificial Intelligence Act 2026** across real-time SEPA Instant and card acquiring workflows.

Built from a **Head of Security / Head of ICT & InfoSec Risk** perspective, this repository moves beyond static policy checklists—defining **closed-loop operational workflows**, **hard engineering decision gates**, **result-oriented SLA/KRI matrices**, and **executable validation scripts**.

---

## 1. Closed-Loop Digital Operational Resilience Architecture

```mermaid
flowchart TD
    P1["<b>Pillar 1: Resilience Governance &amp; Impact Tolerances</b><br/>DORA Ch. II · CBI OpRes Guidance · IAF/SEAR<br/><i>IBS Mapping · SEPA RTO 30m · Safeguarding RTO 2h</i>"]

    P2["<b>Pillar 2: ICT Protection &amp; Change Gates</b><br/>DORA Art. 7–14 · PCI-DSS v4.0 · EU AI Act Art. 15<br/><i>CMDB Tagging · CI/CD Gates · 7-Day Critical Patch SLA</i>"]

    P5["<b>Pillar 5: ICT Third-Party Risk &amp; DORA RoI</b><br/>DORA Ch. V · EBA DPM 4.0 · CBI Outsourcing<br/><i>CIF Intake · XBRL RoI Validator · Exit Tabletop Drills</i>"]

    P3["<b>Pillar 3: Detection &amp; 4-Hour CBI Incident Engine</b><br/>DORA Ch. III · RTS on Major Incidents<br/><i>SIEM Telemetry · 45m RTS Triage · 4h CBI Portal Clock</i>"]

    P4["<b>Pillar 4: Resilience Testing &amp; TIBER-IE</b><br/>DORA Ch. IV · TIBER-IE Framework<br/><i>Quarterly BCDR Failover · Red-Team TLPT Closure</i>"]

    P6["<b>Pillar 6: Threat Intel, Payments &amp; AI Controls</b><br/>DORA Ch. VI · PSD3/PSR · CBI Safeguarding · EU AI Act<br/><i>FS-ISAC Feeds · Daily D+1 Ledger Checks · AI Guardrails</i>"]

    P1 --> P2
    P1 --> P5
    P2 --> P3
    P5 --> P3
    P3 --> P4
    P4 -.->|Tolerance Calibration| P1
    P6 <--> P2
    P6 <--> P3
```

## 2. The 6-Pillar Operating Matrix (Processes, Outcomes & Artifacts)

| Pillar & Repository Module | Regulatory Anchor | Defined End-to-End Process & Gates | Result-Oriented Target Outcomes | Executable / Structured Artifact |
| :--- | :--- | :--- | :--- | :--- |
| **[Pillar 1: Resilience Governance & Impact Tolerances](pillar-01-governance-and-impact-tolerances/README.md)** | **DORA Ch. II (Art. 5–6)**, **CBI OpRes Guidance**, & **CBI IAF / SEAR** | IBS identification → End-to-end dependency mapping → Board Impact Tolerance setting → Time-bound Risk Exception Gate (`<= 90d`). | • SEPA Instant RTO `< 30m` (RPO `0` txn loss)<br>• `100%` of risk exceptions tied to PCF owner & expiry | `ibs-impact-tolerance-model.yaml` |
| **[Pillar 2: ICT Protection & Change Control](pillar-02-ict-protection-and-change-control/README.md)** | **DORA Ch. II (Art. 7–14)**, **PCI-DSS v4.0**, & **EU AI Act Art. 15** | Asset-to-IBS tagging → Automated CI/CD & AI-egress gates → EPSS/CVSS triage → Patch SLA enforcement & virtual patch fallback. | • Critical (`CVSS >= 9.0`) patched `< 7d` (`>= 95%` SLA)<br>• `0` unencrypted CDE/PII stores in production | `sla-breach-detector.py` |
| **[Pillar 3: Incident Response & CBI 4-Hour Clock](pillar-03-incident-response-and-cbi-reporting/README.md)** | **DORA Ch. III (Art. 17–23)** & **DORA RTS on Major Incidents** | Alert trigger → 30m technical triage → 45m quantitative RTS threshold gate → CBI Portal initial notice (`< 4h`), `72h` intermediate, `30d` RCA. | • Mean Time to Classify (MTTC) `< 45 mins`<br>• `100%` on-time CBI statutory portal submissions | `dora-incident-classifier.py` |
| **[Pillar 4: Resilience Testing & TIBER-IE](pillar-04-resilience-testing-and-tiber-ie/README.md)** | **DORA Ch. IV (Art. 24–27)** & **TIBER-IE Framework** | Annual risk-based test plan → Quarterly BCDR failover drills → **TIBER-IE** red-team scoping, purple-team replay & closure gate. | • Failover recovery `<= 75%` of Impact Tolerance<br>• `100%` of TIBER-IE critical findings closed `< 60d` | `bcdr-test-scorecard.json` |
| **[Pillar 5: Third-Party Risk & DORA RoI](pillar-05-third-party-risk-and-dora-roi/README.md)** | **DORA Ch. V (Art. 28–44)**, **EBA DPM 4.0**, & **CBI Outsourcing** | Intake & CIF triage → Art. 30 contractual gate → EBA XBRL RoI schema validation → Concentration scoring → Annual stressed exit drill. | • Onboarding SLA reduced from `25d` to `<= 7d`<br>• `0` EBA/CBI Portal XBRL validation rejections | `dora-roi-validator.py` |
| **[Pillar 6: Threat Intel, Payments & AI Controls](pillar-06-threat-intel-payments-and-ai/README.md)** | **DORA Ch. VI**, **PSD3 / PSR**, **CBI Safeguarding**, & **EU AI Act** | Threat feed ingestion → Daily `D+1` safeguarding ledger reconciliation → Verification of Payee (VoP) logging → AI Annex III & Art. 50 guardrails. | • `0` unresolved safeguarding breaks `> €0.01` past `T+1`<br>• Fraud AI human override `< 15m` (`>= 98%` SLA) | `safeguarding-ledger-invariants.sql` |

---

## 3. Executive Outcome Scorecard (Board Risk Appetite Benchmarks)

| Governance Dimension | Baseline (Legacy / Manual) | Target Operating State | Supervisory / Audit Proof |
| :--- | :--- | :--- | :--- |
| **CBI DORA Register of Information (RoI)** | Manual spreadsheet aggregation; high risk of LEI/parent validation errors during March CBI Portal window | Automated ingestion pipeline with pre-submission XBRL/LEI validation (`0` EBA rejections) | Annual **CBI Portal XBRL Return** & **CBI ICT-SAT** evidence pack |
| **Safeguarding Account Integrity (PCF-56)** | End-of-month manual bank statement checks; risk of negative sub-ledger netting | Automated daily `camt.053` reconciliation with hard DB schema floor (`balance >= 0.00`) | Daily immutable reconciliation logs & annual **ISAE 3000** reasonable assurance report |
| **Major ICT Incident Classification** | Ad-hoc severity calls risking breach of DORA's 4-hour initial CBI reporting clock | Deterministic RTS threshold calculator triggered within 45 minutes of detection | Timestamped triage logs & CBI Portal submission receipts |
| **Enterprise AI & Shadow AI Governance** | Uninventoried SaaS AI features; unclear Annex III credit vs. fraud classification | Central AI Inventory mapped to **Regulation of AI Act 2026**, **Art. 50** disclosures live, egress DLP enforced | **CBI Market Surveillance** readiness pack & human-override audit trail |

---

## 4. Industry Reference Frameworks & Community Benchmarks
This operating blueprint aligns with Irish/EU supervisory standards and benchmarks against open-source security governance resources:
* **Supervisory & Technical Standards:** Central Bank of Ireland **ICT Self-Assessment Tool (ICT-SAT)**, **TIBER-IE** Threat-Led Penetration Testing Framework, **EBA DORA RoI Data Point Model (DPM 4.0)**, and Ireland's **Regulation of Artificial Intelligence Act 2026** (*Oifig IS na hÉireann*).
* **Community AI Governance Reference:** [Taimur Ijlal — AI Governance Repository](https://github.com/taimurijlal/AIGovernance) *(Benchmarked for general AI policy structure, model risk checklists, and ISO/IEC 42001 alignment concepts).*

<script type="module">
  import mermaid from '[https://cdn.jsdelivr.net/npm/mermaid@11/dist/mermaid.esm.min.mjs](https://cdn.jsdelivr.net/npm/mermaid@11/dist/mermaid.esm.min.mjs)';
  mermaid.initialize({ startOnLoad: false, theme: 'default' });
  document.querySelectorAll('pre > code.language-mermaid, .language-mermaid pre code').forEach((el) => {
    const container = el.closest('div.language-mermaid') || el.parentElement;
    const div = document.createElement('div');
    div.className = 'mermaid';
    div.textContent = el.textContent;
    container.replaceWith(div);
  });
  await mermaid.run();
</script>
