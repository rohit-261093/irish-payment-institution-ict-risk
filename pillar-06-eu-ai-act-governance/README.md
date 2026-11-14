---
title: Pillar 6 — EU AI Act Deployer Governance & Ireland Regulation of Artificial Intelligence Act 2026
---

# Pillar 6: EU AI Act Deployer Governance & Irish AI Act 2026
**Regulatory Basis:** EU Artificial Intelligence Act (Regulation (EU) 2024/1689 — Article 26 Deployer Obligations) · Ireland Regulation of Artificial Intelligence Act 2026 (Commenced 31 July 2026) · Central Bank of Ireland (CBI) Regulatory & Supervisory Outlook (February 2026)

---

## 1. What Pillar 6 Means in Practice (100% Third-Party AI Deployer Model)
The Payment Institution **does not train, fine-tune, or develop proprietary AI models in-house**. Every AI capability used across payment rails, onboarding, and operations is procured from third-party vendors (linked directly to the **Pillar 5 DORA Register of Information**), positioning the firm strictly as an **AI Deployer** under **Article 3(4) and Article 26 of the EU AI Act**.

Under **Ireland's Regulation of Artificial Intelligence Act 2026**, the **Central Bank of Ireland (CBI)** supervises and enforces AI compliance across regulated financial services firms using its Administrative Sanctions Procedure and **Individual Accountability Framework (IAF/SEAR)**. Operating as a disciplined **AI Deployer** requires four operational controls:
1. **Preventing Accidental "Provider" Reclassification (`Article 25`):** Never rebranding a third-party high-risk AI tool under the Payment Institution's own trademark or modifying its intended purpose, which would legally shift full `Provider` conformity obligations onto the firm.
2. **Article 26 Deployer Duties & Vendor Audit Assurance:** Operating third-party AI strictly within the vendor's `Article 13` instructions for use, ensuring clean and representative input data, and collecting quarterly/annual vendor bias, accuracy, and conformity audit packs.
3. **Article 27 FRIA, Human Oversight & Article 50 Transparency:** Separating excluded fraud/AML models (`Annex III Point 5(b)` carve-out) from high-risk third-party merchant underwriting and biometric eKYC APIs (`FRIA` + human review SLAs), while enforcing `Article 50` disclosures on customer-facing support chatbots.
4. **Article 26(5) Serious Incident Suspension & SaaS GenAI DLP:** Maintaining a kill-switch to suspend a third-party AI API and notify the vendor and CBI if output anomalies or bias spikes emerge, while blocking unsanctioned Shadow AI at the proxy.

---

## 2. Regulatory Alignment Matrix (EU AI Act Deployer Duties & CBI Outlook)

| Regulatory Anchor | Specific Deployer Requirement | How Pillar 6 Operationalises It |
| :--- | :--- | :--- |
| **Irish AI Act 2026** & **CBI Feb 2026 Outlook** | Maintain an up-to-date register of all third-party AI systems, risk tiers, and accountable PCF/executive owners. | **`EU_AI_Act_System_Inventory`:** Inventories all deployed SaaS/API AI tools (`0` in-house trained models) mapped to `CIBS` and PCF owners. |
| **EU AI Act Art. 5, Art. 25 & Annex III** | Block prohibited AI (`Art. 5`); avoid `Art. 25` rebranding; distinguish excluded fraud/AML APIs from `Annex III` high-risk APIs. | **`EU_AI_Act_System_Inventory`:** Enforces `Deployer` role discipline and flags `AI-002` (Underwriting) & `AI-004` (Biometric eKYC) as high-risk. |
| **EU AI Act Art. 26(1)–(4) & Art. 27** | Follow vendor instructions for use, assign trained human oversight, and complete an `Art. 27` FRIA before high-risk go-live. | **`Art26_Deployer_And_FRIA_Gate`:** Pre-production gate verifying vendor `Art. 13` instructions, `DPIA + FRIA`, and human override queues. |
| **EU AI Act Art. 26(5) & Art. 73** | Monitor third-party AI outputs; suspend use and notify the vendor and CBI if serious risk or malfunction arises. | **`Quarterly_Vendor_AI_Assurance` & `Art26_Deployer_And_FRIA_Gate`:** Tracks local false-positive/reject rates and `60-second` API kill-switches. |
| **EU AI Act Art. 4 & Art. 50** | Ensure staff AI literacy (`Art. 4`), display chatbot disclosures (`Art. 50`), and prevent `PAN`/`PII` leakage to external LLMs. | **`GenAI_And_Shadow_AI_Gate`:** Enforces `ZDR` EU endpoints, `PAN`/`PII` egress redaction, and CASB blocking of Shadow AI. |

---

## 3. End-to-End Third-Party AI Deployer Lifecycle & Hard Gates

1. **Step 1 — Vendor AI Intake & Role/Risk Triage (`Linked to Pillar 5 Onboarding`):**
   * Before procuring any SaaS tool or API containing AI, 2nd Line ICT Risk and Compliance classify the system in **`EU_AI_Act_System_Inventory`** as `Deployer`.
   * **Hard Gate:** Any tool involving `Article 5` prohibited practices or attempting to rebrand a high-risk third-party model under the firm's name (`Article 25`) is rejected.
2. **Step 2 — Article 26 Instructions, FRIA & Article 50 Transparency Gate (`Pre-Go-Live`):**
   * 2nd Line ICT Risk and the DPO verify the vendor's `Article 13` instructions for use, complete `DPIA + Article 27 FRIA` for high-risk underwriting/biometric APIs, and verify `Article 50` chatbot UI disclosures in **`Art26_Deployer_And_FRIA_Gate`**.
   * **Hard Gate:** Production API keys cannot be enabled until `Deployer Gate Verdict` reads `VERIFIED`.
3. **Step 3 — Quarterly Vendor Assurance & Local Output Monitoring (`90-Day Cycle`):**
   * System owners and 2nd Line Risk review the vendor's latest SOC 2 / fairness & bias audit pack alongside local false-positive/reject rates and API reason-code explainability in **`Quarterly_Vendor_AI_Assurance`**.
   * **Hard Gate:** Any vendor failing to supply updated bias/conformity assurance or breaching local false-positive thresholds triggers vendor escalation and fallback to deterministic rules.
4. **Step 4 — Serious AI Incident Suspension (`Article 26(5)` & `Pillar 3 CBI Clock`):**
   * If a third-party AI API causes discriminatory rejections, blocks `> 10%` of legitimate payments, or leaks `PII`/`PAN`, engineering triggers the API kill-switch (`<= 60s`), notifies the vendor under `Article 26(5)`, and initiates **Pillar 3's 4-hour CBI incident reporting clock**.

---

## 4. RACI & Accountability Matrix (AI Deployer Model)

| Third-Party AI Governance Activity | Board Risk Committee | PCF-52 (MLRO) / CRO / CTO | Engineering & Ops Teams | DPO & Legal | Head of ICT & InfoSec Risk (2nd Line) |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Enterprise AI Policy & Art. 4 Staff AI Literacy** | **A** | **C** | **I** | **C** | **R** |
| **Third-Party AI Inventory & Risk Classification** | **I** | **C** | **C** | **C** | **A / R** |
| **Art. 26 Vendor Instructions & Art. 27 FRIA Sign-Off** | **I** | **A (Business Owner)** | **C** | **R (DPIA/FRIA)** | **R (ICT/Vendor Risk)** |
| **Art. 50 Chatbot Disclosures, ZDR Proxy & Shadow AI** | **I** | **C** | **R** | **C** | **A** |
| **Human-in-the-Loop Override Queues & API Kill-Switch** | **I** | **A (PCF Owner)** | **R** | **I** | **C (2nd Line Challenge)** |
| **Quarterly Vendor Bias/Audit Pack & Output Review** | **I** | **A (System Owner)** | **R** | **I** | **C (2nd Line Sign-Off)** |

*(**R** = Responsible, **A** = Accountable, **C** = Consulted, **I** = Informed)*

---

## 5. Target AI Deployer KPIs

| Metric / Outcome | Target Benchmark | How It Is Measured |
| :--- | :--- | :--- |
| **Third-Party AI Inventory Completeness** | `100%` of vendor AI tools classified prior to production API activation (`0` in-house trained models) | `EU_AI_Act_System_Inventory` vs. Pillar 5 DORA RoI |
| **Art. 26 Instructions, FRIA & Art. 50 Gate** | `100%` of `Annex III` APIs have signed FRIAs; `100%` of chatbots display `Art. 50` notices | `Deployer Gate Verdict` in `Art26_Deployer_And_FRIA_Gate` |
| **Human-in-the-Loop Override SLA** | `>= 98%` of automated blocks/declines reviewed within `15–60 mins` | `Actual Override SLA %` in `EU_AI_Act_System_Inventory` |
| **Quarterly Vendor Assurance Currency** | `100%` of vendor bias/audit packs & local output rates reviewed every `90 days` | `Deployer Assurance Verdict` in `Quarterly_Vendor_AI_Assurance` |
| **Shadow AI Containment** | `0` unsanctioned SaaS GenAI tools permitted to process customer `PII` or card `PAN` | `Security Verdict` in `GenAI_And_Shadow_AI_Gate` |

---

## 6. Supporting Excel Registers
All third-party AI system classifications, Article 26 deployer gates, quarterly vendor audit reviews, and SaaS GenAI DLP controls are maintained across two companion Excel workbooks in this folder:

1. **[`pillar-06-eu-ai-act-inventory-and-fria.xlsx`](pillar-06-eu-ai-act-inventory-and-fria.xlsx)**
   * **`AI_Governance_Dashboard`:** Executive KPI cards confirming `0` in-house trained models and tracking deployed third-party AI tools.
   * **`EU_AI_Act_System_Inventory`:** Master CBI-ready Deployer register mapping `Annex III` high-risk, excluded fraud/AML APIs, `Art. 50` chatbots, and human-override SLAs.
   * **`Art26_Deployer_And_FRIA_Gate`:** Pre-release gate verifying vendor `Art. 13` instructions for use, `Art. 27` FRIAs, `Art. 50` disclosures, and `Art. 26(5)` incident triggers.
2. **[`pillar-06-vendor-ai-assurance-and-llm-dlp.xlsx`](pillar-06-vendor-ai-assurance-and-llm-dlp.xlsx)**
   * **`Vendor_AI_And_DLP_Dashboard`:** Quarterly vendor assurance and Shadow AI containment KPIs.
   * **`Quarterly_Vendor_AI_Assurance`:** `90-day` Deployer assurance register tracking vendor bias/conformity audit packs, local false-positive rates, and API reason codes.
   * **`GenAI_And_Shadow_AI_Gate`:** Governance register enforcing `ZDR` EU endpoints, `PAN`/`PII` egress redaction, and CASB Shadow AI blocking.
