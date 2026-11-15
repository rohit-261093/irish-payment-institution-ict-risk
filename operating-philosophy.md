---
title: Operating Philosophy & Risk Decision Framework
---

# Operating Philosophy & Risk Decision Framework
### How ICT Risk, Operational Resilience & AI Governance Work in Practice

Governance frameworks fail when they become static binders of rules that engineering teams work around and executives only read before an inspection. This document defines the **core operating philosophy and decision-making framework** behind the 6 pillars in this repository—explaining how risks are prioritized, how trade-offs are made under pressure, and how regulatory mandates (**DORA**, **Central Bank of Ireland Operational Resilience & Outsourcing Guidance**, **IAF/SEAR**, and the **EU AI Act / Irish AI Act 2026**) are translated into daily execution.

---

## 1. The Five Core Operating Principles

### Principle 1: Protect Customer Harm & Payment Rails—Not Just Servers
We do not prioritize security and resilience work based on generic technical severity scores alone. Every risk decision starts from external customer impact and market integrity:
* **Impact Tolerances Anchor Everything (`Pillar 1`):** Every asset, cryptographic key, vendor API, and AI tool is mapped to a Board-approved **Critical or Important Business Service (`CIBS-01` to `CIBS-05`)**.
* **Practical Trade-Off Rule:** A `CVSS 7.5` vulnerability on an internet-facing SEPA Instant gateway (`CIBS-01`, `30-minute` impact tolerance) is remediated ahead of a `CVSS 9.8` flaw on an isolated internal marketing test environment.

### Principle 2: Hard Gates Over Passive Policies
Controls that rely on people remembering a 60-page policy during a busy release cycle or a live outage will eventually fail. Wherever possible, governance is embedded directly into existing workflows as **deterministic hard gates**:
* **Change & DLP Gate (`Pillar 2`):** High-risk production releases cannot deploy without verified rollback procedures and automated `PAN`/`PII` egress checks.
* **Incident Clock Gate (`Pillar 3`):** Any disruption touching a `CIBS` triggers a mandatory **45-minute threshold triage** to protect the Central Bank of Ireland's **4-hour initial reporting window**.
* **Vendor & Contract Gate (`Pillar 5`):** Procurement cannot execute a contract or provision production API keys until `Article 30` mandatory clauses (CBI audit rights, EEA residency, exit assistance) are verified.
* **AI Deployer Gate (`Pillar 6`):** Third-party AI APIs cannot go live without `Article 26` vendor instructions verification, `Article 27` FRIAs (where applicable), and `Article 50` customer disclosures.

### Principle 3: Statutory Precision Over "Gold-Plating"
Over-engineering compliance where the law does not require it burns engineering capacity and slows down product delivery. We apply strict legal and architectural precision so controls remain proportionate:
* **100% Third-Party AI Deployer Focus (`Pillar 6`):** Because the institution **does not train or develop proprietary AI models in-house**, we do not build unnecessary model-training bureaucracy. Instead, we focus rigorously on **EU AI Act Article 26 Deployer duties**—preventing accidental `Article 25` reclassification as a Provider, separating excluded fraud/AML APIs (`Annex III Point 5(b)` carve-out) from high-risk credit and biometric eKYC APIs, and enforcing `15–60 minute` human override SLAs.
* **Tiered Third-Party Scrutiny (`Pillar 5`):** Deep fourth-party hyperscaler concentration analysis and annual stressed exit tabletop drills are concentrated on `CIF`-critical providers rather than low-risk back-office SaaS tools.

### Principle 4: Separate Technical Recovery from Regulatory Command in a Crisis
During a severe outage—such as a core payment rail degradation or an enterprise-wide Microsoft 365 / Outlook outage—engineers cannot simultaneously debug root causes, calculate DORA reporting thresholds, and field client escalations:
* **Parallel Tracks (`Pillar 3`):** 1st Line Engineering focuses 100% on technical containment and failover, while 2nd Line ICT Risk, Compliance, and Crisis Management run the **45-minute regulatory clock**, activate out-of-band communication channels, and enforce pre-approved manual workarounds.
* **Stopping Improvised Risk:** During communication outages, staff are explicitly prohibited from improvising workarounds (such as routing payment instructions via personal email or unapproved messaging apps), backed by active CASB and DLP controls.

### Principle 5: Translate Risk Both Ways—Engineering & The Board
Effective risk leadership requires translating technical reality into clear executive trade-offs without losing precision:
* **To Engineering & Product:** Regulatory articles are translated into concrete engineering tickets, patch SLAs (`<= 7 days` for critical/KEV flaws), failover margins (`<= 75%` of Board RTO), and API kill-switches.
* **To the Board & PCF Holders (`IAF / SEAR`):** Technical telemetry is distilled into **risk appetite breaches, residual risk trends, overdue CAPAs, and cost-vs-resilience decisions**—giving Pre-Approval Controlled Function (`PCF`) holders clear, auditable evidence to discharge their statutory accountability.

---

## 2. The Risk Prioritization & Decision Matrix

When competing priorities, audit findings, or operational incidents arise, decisions are triaged using the four-tier model below:

| Priority Tier | Trigger Condition | Required Decision & Escalation Path | Maximum SLA |
| :--- | :--- | :--- | :--- |
| **Tier 1: Immediate Stop / Crisis** | Active breach of a `CIBS` Impact Tolerance (`RTO/RPO`), confirmed data/PAN exposure, CISA KEV on an internet-facing `CIBS` asset, or high-risk AI malfunction (`Art. 26(5)`). | Trigger emergency containment / API kill-switch; start **45-min DORA triage**; notify `PCF-1` / `PCF-52` and file **4-hour CBI Portal notice** if thresholds are met. | **Immediate (`<= 45m` triage / `<= 4h` CBI filing)** |
| **Tier 2: Hard Gate Hold** | Missing `DORA Art. 30` contract clause, unapproved `Annex III` AI API without `FRIA`, unauthorized checkout script, or expired `90-day` risk exception. | **Block go-live or contract signature** automatically; escalate to Head of ICT & InfoSec Risk or Board Risk Committee for formal waiver or remediation. | **Blocked until remediated** |
| **Tier 3: Accelerated Remediation** | Critical vulnerability (`CVSS >= 9.0` non-KEV) on `CIBS` infrastructure, BCDR failover drill exceeding `75%` of RTO (`Tight Margin`), or TIBER-IE red-team finding. | Assign 1st Line engineering owner; track in Pillar 2/4 registers; verify closure via **Purple-Team replay** or re-test before closing. | **`<= 7 days` (Critical Vuln)** / **`<= 60 days` (TLPT)** |
| **Tier 4: Planned Hygiene & Governance** | Medium/Low vulnerabilities on non-CIBS assets, annual `ICT-SAT` self-assessments, quarterly PAM recertifications, and rolling `365-day` vendor exit drills. | Execute within standard operational sprints and review quarterly at the Operational Resilience & Risk Committee. | **`30–90 days` (Scheduled)** |

---

## 3. Practical Trade-Offs: How Ambiguity Is Resolved

In day-to-day operations, security and resilience requirements often collide with commercial urgency. Four standing rules govern how trade-offs are resolved:

1. **Speed vs. Control on Vendor Onboarding:** Commercial teams need fast turnaround to sign payment partners and SaaS tools. Rather than holding every vendor for weeks, 2nd Line Risk enforces a **`<= 7 business day` fast-track SLA** for standard reviews—while maintaining an uncompromising **hard stop** on `Article 30` audit rights, EEA data residency, and `Zero-Data-Retention` AI terms.
2. **Temporary Exceptions vs. Permanent Risk Acceptance:** When a deadline cannot be met (for example, a legacy vendor API delay), the business may request a **Risk Exception (`Pillar 1`)**—capped strictly at **90 days** with compensating controls. No exception can roll over silently; any renewal past 90 days requires explicit **Board Risk Committee** sign-off.
3. **Automation vs. Human Oversight in AI:** Real-time fraud and AML screening (`AI-001`, `AI-005`) must operate at millisecond speed to protect SEPA Instant rails, whereas high-risk underwriting (`AI-002`) and biometric onboarding (`AI-004`) require deterministic **human-in-the-loop review queues (`15–60 mins`)** and instant fallback to deterministic rules if model anomalies occur.
4. **Testing in Production vs. Operational Stability:** Resilience testing (`Pillar 4`) must prove real failover capability—not just tabletop theory—so active-active failover drills and TIBER-IE red-team exercises are executed against production-equivalent or live rails under strict **Rules of Engagement**, pre-vetted `Article 27` testers, and instant abort triggers.

---

## 4. How This Philosophy Connects to the 6 Pillars

* **[Pillar 1: Resilience Governance & Impact Tolerances](pillar-01-governance-and-impact-tolerances/README.md)** — Defines *what matters most* (`CIBS`), *how much disruption is tolerable* (`RTO/RPO`), and *who is accountable* (`IAF/SEAR`).
* **[Pillar 2: ICT Protection & Change Control](pillar-02-ict-protection-and-change-control/README.md)** — Hardens the underlying assets, cryptographic keys, privileged access, and CI/CD release gates.
* **[Pillar 3: Incident Response & CBI 4-Hour Clock](pillar-03-incident-response-and-cbi-reporting/README.md)** — Governs live crisis execution, deterministic DORA threshold triage, and regulatory/client communications.
* **[Pillar 4: Resilience Testing & TIBER-IE TLPT](pillar-04-resilience-testing-and-tiber-ie/README.md)** — Proves empirically through failover drills and intelligence-led red-teaming that tolerances hold under stress.
* **[Pillar 5: Third-Party Risk & DORA RoI](pillar-05-third-party-risk-and-dora-roi/README.md)** — Extends resilience and contractual control across critical cloud, banking, and SaaS dependencies.
* **[Pillar 6: EU AI Act Deployer Governance](pillar-06-eu-ai-act-governance/README.md)** — Applies proportionate, deployer-specific oversight, `FRIA` gates, and egress DLP across third-party AI capabilities.
