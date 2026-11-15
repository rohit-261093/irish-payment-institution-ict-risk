---
title: IRP-03 — Enterprise Microsoft 365 / Exchange Online (Outlook) Outage Playbook
---

# IRP-03: Enterprise Microsoft 365 / Exchange Online (Outlook) Outage
**Playbook ID:** `IRP-03` · **Primary Pillar:** Pillar 3 (`pillar-03-incident-response-and-cbi-reporting/`) · **Linked Registers:** [`pillar-03-dora-incident-cbi-clock.xlsx`](../pillar-03-dora-incident-cbi-clock.xlsx) & [`pillar-05-dora-roi-and-concentration.xlsx`](../../pillar-05-third-party-risk-and-dora-roi/pillar-05-dora-roi-and-concentration.xlsx)

---

## 1. Trigger & Severity Classification (`T+0`)

### Activation Triggers
Activate `IRP-03` immediately upon any of the following conditions:
* **Exchange Online / Outlook Service Loss:** Enterprise-wide inability to send, receive, or authenticate into Microsoft Outlook / Exchange Online across corporate operations for `> 15 minutes` (confirmed via Microsoft 365 Service Health or internal synthetic probes).
* **Entra ID / SSO Dependency Cascade:** Microsoft Entra ID authentication degradation blocking staff access to downstream treasury, client onboarding, or safeguarding portals.
* **Mail Gateway Spooling Alert:** Proofpoint / Mimecast Secure Email Gateway reports inbound/outbound mail queuing or deferral spikes `> 500` messages.

### Statutory & Operational Impact Mapping
* **Why Outlook Is High-Risk in a Payment Institution:** While core payment rails (`CIBS-01`, `CIBS-02`) run on isolated cloud APIs, email frequently acts as an informal intake channel for client payment instructions, treasury wire sign-offs, safeguarding bank advisories (`CIBS-03`), and KYC document submissions (`CIBS-04`).
* **DORA `RTS 2024/1772` & Third-Party Concentration Link (`Pillar 5`):** A third-party hyperscaler/SaaS outage (Microsoft) triggers the firm's regulatory reporting clock if inability to receive or process client instructions threatens Board-approved Impact Tolerances (`240 mins` for `CIBS-03` / `CIBS-04`) or delays same-day EUR/USD settlement cut-offs.

---

## 2. Out-of-Band Command & Roles (`T+0 to T+15 Mins`)

| Crisis Role | Designated Owner | Primary Responsibility During `IRP-03` |
| :--- | :--- | :--- |
| **Crisis Lead** | Head of ICT & InfoSec Risk | Chairs out-of-band crisis bridge, enforces anti-fraud/Shadow-IT freeze, and runs the **45-minute DORA triage**. |
| **Technical & Identity Lead** | IT Operations Lead & SecOps Lead | Verifies tenant security (ruling out BEC/DNS hijack), monitors mail gateway spooling, and manages Entra ID fallback. |
| **Treasury & Operations Lead** | Head of Payments Ops / Safeguarding (`PCF-56`) | Redirects urgent client payment instructions to the MFA-authenticated Client Portal and enforces dual-control callbacks. |
| **Regulatory & Vendor Lead** | Head of Compliance (`PCF-52`) & Vendor Manager | Logs Microsoft Severity A ticket (`DORA RoI`), tracks CBI 4-hour clock, and approves client status notices. |

* **Out-of-Band Command Rule:** **Do not rely on Microsoft Teams or Outlook for crisis coordination.** Immediately open the pre-configured **Slack Enterprise Grid `#crisis-m365-outage` channel** and the **Signal Executive Bridge** (distributed via SMS alert).

---

## 3. Immediate Containment & Anti-Fraud Guardrails (`T+15 to T+45 Mins`)

1. **Rule Out Tenant Compromise vs. Benign Vendor Outage (`DORA Art. 17`):**
   * Within `15 minutes`, SecOps inspects Entra ID sign-in logs, DNS `MX`/`SPF`/`DKIM` records, and Microsoft Defender alerts to verify the outage is an upstream Microsoft service disruption rather than a tenant-level Business Email Compromise (**BEC**) or DNS hijack.
2. **Issue Mandatory Anti-Fraud & Shadow-IT Freeze (All Staff):**
   * Broadcast an immediate SMS and Intranet banner to all staff enforcing two strict rules:
     * **Zero Personal Email / Consumer Messaging:** Staff are strictly prohibited from forwarding client instructions, NAV/ledger files, or PII to personal Gmail/Outlook accounts or consumer WhatsApp/Telegram chats (`Pillar 2` & `Pillar 6` DLP/CASB enforcement).
     * **Heightened Callback Fraud Vigilance:** Threat actors actively exploit public M365 outages to spoof urgent "workaround payment" emails or phone calls. Treasury must apply **100% out-of-band phone verification** against pre-registered client numbers for any urgent payment request.
3. **Verify Secure Email Gateway Spooling:**
   * Confirm Proofpoint / Mimecast is holding all inbound external emails in an encrypted spool queue with **zero bounces/NDNs** sent to clients or depositary banks, and activate emergency webmail continuity portals if provisioned.

---

## 4. The Regulatory & Client Notification Clock (`T+45 Mins to T+30 Days`)

Log all assessment milestones in [`pillar-03-dora-incident-cbi-clock.xlsx`](../pillar-03-dora-incident-cbi-clock.xlsx):

* **`T + 45 Minutes` (Hard Gate — DORA RTS Triage):**
  * Head of ICT Risk evaluates whether the email/Entra ID outage is preventing `CIBS-03` (Safeguarding) or `CIBS-04` (Onboarding/Client Instructions) from meeting daily settlement cut-offs or breaching the `240-minute` Impact Tolerance.
  * If thresholds are met (or likely to breach before Microsoft's published ETA), escalate to `PCF-1` (CEO) and `PCF-52` (MLRO).
* **`<= 4 Hours from Classification` (CBI Portal Initial Notification):**
  * If classified **Major** under `RTS 2024/1772`, `PCF-52` files the **DORA Article 19(4)(a) Initial Notification** via the CBI Portal, identifying Microsoft as the third-party ICT provider (`Pillar 5 DORA RoI`).
* **`<= 2 Hours` (Proactive Client & Banking Partner Notice — `DORA Art. 19(3)`):**
  * Publish an advisory on `status.fintech.ie` and the authenticated Client Portal confirming that core payment rails (`CIBS-01`/`CIBS-02`) are unaffected and directing clients to submit time-critical payment instructions via the **Client Portal** rather than email.
* **`<= 72 Hours` & `<= 30 Calendar Days` (Intermediate & Final CBI Reports):**
  * Submit intermediate status updates (`72h`) and the final post-incident report (`30d`) incorporating Microsoft's official Post-Incident Review (**PIR**).

---

## 5. Business Continuity Workaround Handoff (`BCP`)

While Exchange Online remains unavailable:
1. **Client Instruction Intake (`CIBS-01` / `CIBS-03`):** All corporate clients and merchants submit urgent payment files, FX instructions, and beneficiary updates exclusively through the **MFA-authenticated Client Portal** or direct **SFTP / API** channels.
2. **Safeguarding & Treasury Approvals (`PCF-56`):** Treasury pulls pending settlement queues directly from the Core Accounting Ledger (`CIBS-03`) and executes dual-control sign-off inside the banking portal (`AIB` / `BOI`) rather than via email approval threads.
3. **KYC / Onboarding Submissions (`CIBS-04`):** Customer Operations directs applicants to upload verification documents directly via the encrypted Client Portal upload widget (`VeriID` workflow) instead of email attachments.

---

## 6. Recovery Verification & Post-Incident Closure (`T+Recovery to T+30 Days`)

1. **Controlled Mail Queue Drain & Duplicate-Payment Prevention:**
   * When Microsoft restores Exchange Online, release spooled messages from the Secure Email Gateway in controlled batches.
   * Payments Operations and Treasury must perform a **100% reconciliation** comparing every email instruction that arrived during the outage against payments already executed via the Client Portal workaround—preventing duplicate wire transfers.
2. **CAPA & Concentration Risk Review (`Pillar 3`, `Pillar 4` & `Pillar 5`):**
   * Log any operational gaps in [`pillar-03-crisis-comms-and-capa-log.xlsx`](../pillar-03-crisis-comms-and-capa-log.xlsx) (`RCA_And_CAPA_Closure_Log`), accelerating the migration of any remaining email-based payment workflows onto structured API/portal rails.
   * Update Microsoft's incident history and concentration risk scoring in **Pillar 5 (`DORA_RoI_Master_Register`)**.
