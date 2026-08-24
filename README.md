# Automated ServiceNow SAR Approvals (ASAP v1.0)

![Automation Anywhere](https://img.shields.io/badge/Platform-Automation_Anywhere_A360-orange?style=flat-square)
![ServiceNow](https://img.shields.io/badge/Integration-ServiceNow_Inbound_Email-green?style=flat-square)
![Outlook](https://img.shields.io/badge/Mail-Microsoft_Outlook-blue?style=flat-square)
![Status](https://img.shields.io/badge/Status-Production_Ready-success?style=flat-square)

Headless enterprise task bot built in Automation Anywhere A360 to automate manual Service Access Request (SAR) approvals in ServiceNow, replacing UI-based interactions with ServiceNow's native inbound email gateway processing.

---

## 📌 Project Overview

Processing manual Service Access Requests (SAR) via a browser UI introduces DOM dependencies, session timeouts, and execution latency. The **Automated SAR Approval Process (ASAP)** bot monitors incoming approval notifications in Microsoft Outlook, parses critical metadata, and responds via ServiceNow's inbound email gateway to complete approvals headlessly.

* **Iteration 1 (UI-Based):** Initial version used browser automation and simulated keystrokes. While functional, UI loading latencies created execution overhead (~30s runtime per request) and brittle web element dependencies.
* **Iteration 2 (Headless Email Gateway):** Shifted to ServiceNow’s inbound email processor, eliminating browser dependencies entirely and reducing processing runtime by **~95% (1–2s per request)**.

Upon receiving the automated response, ServiceNow advances the approval state and triggers downstream Active Directory (AD) group provisioning.

---

## 🏗 System Architecture & Workflow

```text
[ Outlook Inbox ] ──► ( Unread SAR Email )
                            │
                            ▼
           [ A360 Task Bot: String Extraction ]
           ├── Extract SAR ID, User Name, Profile, Ref ID
           └── Isolate `sys_id` from Query Parameter URL
                            │
                            ▼
           [ Background Email Dispatch ]
           └── Target: `wpcomain@service-now.com`
                            │
                            ▼
           [ ServiceNow Inbound Processor ]
           ├── Advances SAR Approval State
           └── Triggers Downstream AD Group Provisioning
                            │
                            ▼
           [ Post-Processing & Logging ]
           ├── Update Excel Audit Log (`ASAP_AuditLog_$sBotRunDate$.xlsx`)
           ├── Write Execution Log (`ASAP_ExecutionLog_$sBotRunDate$.txt`)
           └── Archive Email ──► `Inbox/Bot Processed SARs`
