---
title: Enterprise AI Inventory & EU AI Act Risk Classification Register
---

# Enterprise AI System Inventory & EU AI Act Classification Register
**Entity Profile:** Irish-Authorised Payment Institution (PI/EMI)  
**Owner:** Head of ICT & InfoSec Risk (2nd Line of Defence)  
**Supervisory Authorities:** Central Bank of Ireland (Sectoral Market Surveillance Authority) & Irish AI Office (*Oifig IS na hÉireann*)  

---

## 1. Regulatory & Supervisory Context (Ireland)
Under the **EU AI Act (Regulation (EU) 2024/1689)**, the **2026 EU AI Omnibus**, and Ireland's **Regulation of Artificial Intelligence Act 2026**, financial services firms must maintain a living inventory of all in-house and third-party embedded AI systems:
* **Active Obligations (In Force):** **Article 5** prohibited practices, **Article 4** role-appropriate AI literacy, and **Article 50** transparency rules for customer-facing chatbots and synthetic content.
* **High-Risk Deadline (2 December 2027):** Full **Annex III** high-risk obligations (risk management system, data governance, technical documentation, logging, human oversight, and **Article 27 Fundamental Rights Impact Assessments**) apply to standalone high-risk financial AI systems such as creditworthiness scoring.
* **Key Legal Distinction (Credit vs. Fraud):** Under **Annex III, Point 5(b)**, AI systems evaluating creditworthiness (e.g., Buy-Now-Pay-Later) are **High-Risk**, whereas AI systems used strictly for **detecting financial fraud** are explicitly excluded from Annex III high-risk classification—though they remain governed under **DORA** (ICT change/third-party resilience), **PSD2/PSR** transaction monitoring, and **GDPR Article 22** automated decision-making safeguards.

---

## 2. Production AI System Inventory & Risk Tiering

| System ID | System / Use Case | Role | EU AI Act Tier | Cross-Regulatory Overlap | PCF / Executive Owner | Mandatory Guardrail & Kill-Switch |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **AI-001** | **Real-Time SEPA & Card Fraud Scoring Engine** | Deployer (Vendor SaaS) | **Excluded from Annex III High-Risk** *(Art. 6 / Annex III 5b fraud carve-out)* | **DORA** (CIF Third-Party), **PSD2/PSR**, **GDPR Art. 22** | Head of Financial Crime & Fraud | Sub-second scoring; automated step-up SCA or soft-block with **15-minute analyst override SLA** for false positives. |
| **AI-002** | **Merchant Cash Advance / BNPL Credit Scoring** | Provider / Deployer | **High-Risk** *(Annex III, Point 5b — Creditworthiness)* | **CBI Consumer Protection**, **GDPR Art. 22**, **Art. 27 FRIA** | Chief Credit & Risk Officer | Full Annex III QMS, bias/drift testing on Irish/EEA demographics, **Article 27 FRIA**, and mandatory human underwriter sign-off on declines. |
| **AI-003** | **Customer Payment Dispute & Support Chatbot** | Deployer (LLM Wrapper) | **Limited Risk** *(Article 50 Transparency)* | **DORA**, **GDPR Art. 28**, **PCI-DSS v4.0** | Head of Customer Operations | Upfront disclosure that user is interacting with AI (**Art. 50**); strict PII/PAN regex masking before external LLM inference; zero training on customer data. |
| **AI-004** | **Biometric eKYC Liveness & ID Verification** | Deployer (Vendor API) | **High-Risk / Strict Scrutiny** *(Annex III, Point 1 — Biometrics)* | **AML/CTF (CJA 2010)**, **GDPR Art. 9** (Special Category) | Money Laundering Reporting Officer (MLRO) | Verified against **Article 5** prohibited emotion/categorisation bans; manual compliance fallback path if biometric match fails. |
| **AI-005** | **Internal Engineering & Compliance Copilot** | Deployer | **Minimal Risk** *(Internal Productivity)* | **DORA ICT Security**, **IP & Confidentiality Policy** | Chief Technology Officer (CTO) | Enterprise zero-data-retention tenant; DLP blocks source code secrets, private keys, and customer IBAN/card records from prompts. |

---

## 3. Lifecycle Gateways (Before Production Deployment)
No AI model or SaaS feature containing embedded AI can move into production without passing four **2nd Line ICT & AI Risk Gates**:
1. **Use-Case Intake & Annex III Triage:** Formal classification against Prohibited Practices (**Art. 5**), High-Risk (**Annex III**), and Transparency (**Art. 50**) triggers.
2. **DORA & Data Leakage Assessment:** Verification of third-party ICT criticality (linking to the **DORA Register of Information**), data residency (EEA), and zero-retention contractual clauses.
3. **Explainability & Human Oversight Validation:** Documented human-in-the-loop override procedures and adverse-action explanation templates for customers affected by automated payment blocks or credit declines.
4. **Continuous Drift & Incident Monitoring:** Automated alerting on model accuracy degradation or adversarial prompt/evasion attacks fed directly into the **CBI Major ICT Incident Classification workflow**.
