---
title: Operating Philosophy — Why We Work This Way
---

# Operating Philosophy: Why We Work This Way
### Practical Answers on How We Prioritize Risk, Build Controls & Handle Crises

If you are reviewing this repository for the first time, you will see 6 operational pillars, 4 incident playbooks, an executive reporting pack, and 12 Excel registers. This page explains **the thinking behind the system**—why it is built this way and how we make real-world risk decisions.

---

### 1. Why isn't this just a standard set of security policies?
**Because policies don't stop bad releases or broken vendors—hard gates do.**
In a regulated Irish Payment Institution, an 80-page PDF policy sitting on an intranet will not save you during a live payment outage or a Central Bank of Ireland (`CBI`) inspection. Instead, we embed controls directly into daily workflows as **non-negotiable gates**:
* Code cannot ship to production without rollback proof and automated data-leakage (`DLP`) checks (**Pillar 2**).
* A vendor contract cannot be signed until `DORA Article 30` audit rights and exit clauses are verified (**Pillar 5**).
* A third-party AI tool cannot go live without `Article 26` instructions verification and a signed Fundamental Rights Impact Assessment (`FRIA`) where required (**Pillar 6**).

---

### 2. When everything looks urgent, how do you decide what gets fixed first?
**We prioritize by customer harm and payment rail tolerances—not just technical severity scores.**
We do not protect servers in the abstract; we protect **Critical or Important Business Services (`CIBS`)** like SEPA Instant (`30-minute` impact tolerance) and Card Acquiring (`45-minute` tolerance). 
* **Practical example:** A `CVSS 7.5` vulnerability on an internet-facing SEPA Instant gateway gets patched ahead of a `CVSS 9.8` flaw on an isolated internal marketing test server. Every asset, vendor, and AI tool in this repository is tagged to a `CIBS` so engineering and risk teams always know what matters most.

---

### 3. Why are there no model-training or data-science validation logs in the AI pillar?
**Because we are a 100% third-party AI Deployer—and over-engineering wastes time and money.**
We do not train or build proprietary AI models in-house (`0` trained models). Under the **EU AI Act** and **Ireland's Regulation of Artificial Intelligence Act 2026**, that makes us a **Deployer (`Article 26`)**, not a **Provider**.
* Rather than creating fake data-science bureaucracy, **Pillar 6** focuses strictly on what a Deployer actually controls: preventing accidental `Article 25` rebranding, separating fraud/AML tools (carved out under `Annex III Point 5(b)`) from high-risk credit and biometric eKYC APIs, enforcing `15–60 minute` human review queues, collecting quarterly vendor bias/audit packs, and blocking unsanctioned Shadow AI at the network proxy.

---

### 4. What happens when a major outage hits—like a payment rail failure or an enterprise Outlook outage?
**We split technical recovery from regulatory command within the first 15 minutes.**
During a live crisis, engineers cannot simultaneously debug infrastructure, calculate regulatory reporting thresholds, and answer client emails.
* **Track 1 (1st Line Engineering):** Focuses 100% on containment, failover, or hitting the `60-second` API kill-switch (**Pillar 3 Playbooks**).
* **Track 2 (2nd Line Risk & Compliance):** Runs the **45-minute DORA threshold triage** so we never miss the CBI's **4-hour initial reporting clock**, activates out-of-band communication channels (if Microsoft 365/Outlook is down), and enforces a strict freeze against staff improvising workarounds via personal email or unapproved apps.

---

### 5. What happens when a team genuinely cannot meet a security or compliance deadline?
**We allow temporary, transparent exceptions—never silent workarounds.**
Business urgency is real. If a legacy vendor API needs extra time to patch or migrate, the business can request a formal **Risk Exception (`Pillar 1`)**.
* Every exception requires compensating controls and **expires automatically at 90 days**.
* No exception can roll over quietly in the background—anything extending past 90 days requires explicit **Board Risk Committee** approval.

---

### 6. How do you bridge the gap between engineers and the Board (`IAF / SEAR`)?
**By translating the same data into two different languages.**
* **To Engineering & Product:** We translate DORA, CBI guidance, and the EU AI Act into concrete tickets, clear SLAs (`<= 7 days` for critical/KEV patches, `<= 30 minutes` RTO), and automated CI/CD checks.
* **To the Board & PCF Holders (`IAF / SEAR`):** We roll those same metrics up into **10 Enterprise Key Risk Indicators (`executive-reporting/`)** showing whether we are inside Risk Appetite, which `CAPAs` are overdue, and clear evidence so Pre-Approval Controlled Function (`PCF`) holders can prove they took "Reasonable Steps" in their roles.

---

### Where to Go Next
* **[`index.md`](index.md)** — View the master 6-pillar architecture, cross-pillar links, and all 12 Excel registers.
* **[`executive-reporting/`](executive-reporting/README.md)** — See how operational metrics roll up into the Quarterly Board Risk Committee Pack and KRI Scorecard.
* **[`pillar-03-incident-response-and-cbi-reporting/playbooks/`](pillar-03-incident-response-and-cbi-reporting/playbooks/)** — Inspect our step-by-step response playbooks for payment outages, ransomware, M365/Outlook disruptions, and AI malfunctions.
