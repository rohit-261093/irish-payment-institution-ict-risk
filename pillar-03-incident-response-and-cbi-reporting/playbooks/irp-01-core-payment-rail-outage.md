---
title: IRP-01 — Core Payment Rail & Cloud Availability Zone Outage Playbook
---

# IRP-01: Core Payment Rail & Cloud Availability Zone Outage
**Playbook ID:** `IRP-01` · **Primary Pillar:** Pillar 3 (`pillar-03-incident-response-and-cbi-reporting/`) · **Linked Registers:** [`pillar-03-dora-incident-cbi-clock.xlsx`](../pillar-03-dora-incident-cbi-clock.xlsx) & [`pillar-03-crisis-comms-and-capa-log.xlsx`](../pillar-03-crisis-comms-and-capa-log.xlsx)

---

## 1. Trigger & Severity Classification (`T+0`)

### Activation Triggers
Activate `IRP-01` immediately upon any of the following telemetry or operational alerts:
* **SEPA Instant / SCT Clearing Degradation (`CIBS-01`):** API gateway HTTP `5xx` error rate `> 2.0%` for `> 3 consecutive minutes`, P99 transaction latency `> 5,000 ms`, or loss of connectivity to the TIPS / RT1 clearing gateway.
* **Card Authorization & Tokenization Outage (`CIBS-02`):** Card authorization decline rate spiking `> 5.0%` due to infrastructure timeout, or loss of quorum on the primary FIPS 140-3 Cloud HSM cluster.
* **Primary Cloud Region / AZ Failure:** AWS `eu-west-1` (Dublin) Availability Zone degradation impacting core ledger microservices (`CIBS-01`, `CIBS-03`, `CIBS-05`).

### Statutory & Impact Tolerance Mapping
* **Impacted CIBS & Board RTOs (`Pillar 1`):**
  * `CIBS-01` (SEPA Instant & Cross-Border Clearing): **30-minute** Board Impact Tolerance (`RPO = 0` transaction loss).
  * `CIBS-02` (Card Acquiring & Authorization): **45-minute** Board Impact Tolerance (`RPO = 0` transaction loss).
  * `CIBS-03` (Client Safeguarding & Treasury Ledger): **240-minute** Board Impact Tolerance.
* **DORA `RTS 2024/1772` Baseline Classification:** Any unrecovered outage on `CIBS-01` or `CIBS-02` lasting `> 15 minutes` or affecting `> 10%` of daily payment volume is presumed **Major** unless verified otherwise during the 45-minute triage.

---

## 2. Out-of-Band Command & Roles (`T+0 to T+15 Mins`)

| Crisis Role | Designated Owner | Primary Responsibility During `IRP-01` |
| :--- | :--- | :--- |
| **Incident Commander (Technical)** | On-Call Principal SRE / CTO (`PCF-46`) | Leads 1st Line containment, Route53 DNS health-check failover, and HSM/database quorum recovery. |
| **Crisis & Regulatory Lead** | Head of ICT & InfoSec Risk (2nd Line) | Runs the **45-minute DORA RTS triage**, tracks the **4-hour CBI clock**, and chairs executive updates. |
| **Regulatory Filing Officer** | Head of Compliance / MLRO (`PCF-52`) | Reviews and submits Initial (`4h`), Intermediate (`72h`), and Final (`30d`) reports on the **CBI Portal**. |
| **Safeguarding & Treasury Lead** | Head of Safeguarding (`PCF-56`) | Verifies `RPO = 0` ledger integrity and executes depositary bank liquidity/settlement fallbacks. |
| **Client Communications Lead** | Head of Customer Operations | Publishes status page banners and `DORA Art. 19(3)` client/merchant notices. |

* **Command Bridge:** Open `#inc-cibs-rail-outage` in Slack Enterprise Grid + PagerDuty War Room Bridge (out-of-band backup: Signal Executive Group).

---

## 3. Immediate Containment & Technical Failover (`T+15 to T+45 Mins`)

1. **Isolate Root Cause (Infrastructure vs. Cyber Attack):**
   * SecOps checks WAF, CloudTrail, and GuardDuty telemetry within `10 minutes` to confirm the outage is an infrastructure/cloud failure rather than a volumetric DDoS or destructive wiper attack (if malicious intrusion is detected, immediately pivot to **`IRP-02`**).
2. **Execute Active-Active Failover (`Technical Runbook SOP-NET-01`):**
   * Platform Engineering drains traffic from the degraded AWS `eu-west-1` Availability Zone (`TTL = 15s`) and shifts SEPA Instant / Card Authorization pods to healthy AZs or the `eu-central-1` warm standby.
   * For HSM timeouts (`CIBS-02`), verify secondary Cloud HSM cluster key-quorum availability before re-enabling card authorization traffic.
3. **Protect Transaction Integrity (`RPO = 0`):**
   * Place outbound ISO 20022 payment queues into **idempotent hold/buffer mode** during failover to prevent duplicate SEPA Instant credit transfers or double-posting to safeguarded client accounts.

---

## 4. The Regulatory & Client Notification Clock (`T+45 Mins to T+30 Days`)

All timestamps must be logged immediately in [`pillar-03-dora-incident-cbi-clock.xlsx`](../pillar-03-dora-incident-cbi-clock.xlsx) (`DORA_RTS_Threshold_Triage` and `CBI_4h_72h_30d_Tracker` tabs):

* **`T + 45 Minutes` (Hard Gate — DORA Classification):**
  * Head of ICT Risk completes the deterministic `RTS 2024/1772` threshold score (clients affected, EUR value delayed, service downtime vs. `30m`/`45m` RTO).
  * If classified **Major**, notify `PCF-1` (CEO), `PCF-14` (CRO), and `PCF-52` (MLRO) immediately.
* **`<= 4 Hours from Classification` (CBI Portal Initial Notification):**
  * `PCF-52` and Head of ICT Risk submit the **DORA Article 19(4)(a) Initial Notification** via the Central Bank of Ireland Portal (and verify `<= 24 hours` from initial detection).
* **`<= 4 Hours` (Client & Merchant Notification — `DORA Art. 19(3)`):**
  * If payment delays impact external merchants or payment service users, publish an approved status update on `status.fintech.ie` and issue direct webhook/email notices logged in [`pillar-03-crisis-comms-and-capa-log.xlsx`](../pillar-03-crisis-comms-and-capa-log.xlsx).
* **`<= 72 Hours from Initial Notice` (CBI Portal Intermediate Report):**
  * Submit updated impact metrics, root-cause findings, and recovery confirmation under `DORA Article 19(4)(b)`.
* **`<= 30 Calendar Days` (CBI Portal Final Report & RCA):**
  * Submit the complete Root Cause Analysis (`RCA`), quantified financial/client impact, and permanent `CAPA` plan under `DORA Article 19(4)(c)`.

---

## 5. Business Continuity Workaround Handoff (`BCP`)

If automated failover does not restore `CIBS-01` or `CIBS-03` within **20 minutes** (approaching the 30-minute SEPA Instant Impact Tolerance):
1. **Merchant & Client Portal Advisory:** Display an automated banner on the Client Portal advising customers to route urgent time-critical EUR transfers via standard SEPA Credit Transfer (`SCT`) batch cut-offs or pre-agreed treasury fallback channels.
2. **Safeguarding Reconciliation Fallback (`CIBS-03`):** Treasury downloads manual `camt.053` / CSV statements directly from depositary bank portals (`AIB` / `BOI`) to verify end-of-day client safeguarding balances (`PCF-56` sign-off).

---

## 6. Recovery Verification & Post-Incident Closure (`T+Recovery to T+30 Days`)

1. **Idempotent Queue Drain & Reconciliation:**
   * Before declaring `All Clear`, Payments Engineering and Safeguarding (`PCF-56`) reconcile 100% of buffered ISO 20022 `pacs.008` / `pacs.002` messages against the core ledger to confirm zero dropped or duplicated transactions (`RPO = 0`).
2. **Mandatory CAPA & Pillar 4 Feed:**
   * Log all engineering and process remediations in [`pillar-03-crisis-comms-and-capa-log.xlsx`](../pillar-03-crisis-comms-and-capa-log.xlsx) (`RCA_And_CAPA_Closure_Log`) with strict 30-day owners.
   * Update the scenario parameters in **Pillar 4 (`BCDR_Scenario_Scorecard`)** so the exact failure mode is re-tested during the next quarterly failover drill.
