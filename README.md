# Automated ServiceNow SAR Approvals (A360)

## Project Summary
Developed an Automation Anywhere A360 task bot to automate manual Service Access Request (SAR) approvals in ServiceNow. The bot monitors a shared Outlook inbox for unread requests, extracts key details from the email body, and automatically completes the approval step. 

Upon successful approval by the bot, ServiceNow triggers downstream provisioning of the user into the relevant Active Directory (AD) groups.

Because standard web recorders struggled with ServiceNow’s dynamic UI elements, I designed a front-end workaround using simulated keystrokes to navigate the pages. To keep the process traceable, the bot logs each transaction to an Excel spreadsheet and archives processed emails to prevent duplicate runs.

---

## Video Demonstration
* 🎬 [Watch the full automation execution on Google Drive](https://drive.google.com/file/d/1brWtXZy1UXLRTwsMK_kboNeUVVfYZun2/view?usp=sharing)

---

## Key Automation Steps & Logic
1. **Email Monitoring & Data Extraction:** Monitors Outlook for SAR approval emails and parses key parameters (User ID, System Access Level, Approver Details).
2. **Business Rule Validation:** Validates extracted parameters against pre-defined business rules prior to system entry.
3. **ServiceNow Processing:** Navigates ServiceNow and updates/approves the corresponding access request ticket.
4. **Audit Trail & Reporting:** Records transaction timestamps, status codes, and request details into a centralized Excel audit log.
5. **Exception Handling:** Captures malformed requests or network timeouts, logging exceptions for manual review.

---

## Bot Script Breakdown

| Lines 1 - 17 | Lines 17 - 35 | Lines 35 to End |
| :---: | :---: | :---: |
| ![Lines 1-17](media/AutomatedSARApproval_Bot_Screenshot1.png) | ![Lines 17-35](media/AutomatedSARApproval_Bot_Screenshot2.png) | ![Lines 35-End](media/AutomatedSARApproval_Bot_Screenshot3.png) |

---

## Tech Stack & Tools
* **RPA Platform:** Automation Anywhere A360
* **Applications:** ServiceNow, Microsoft Outlook, Microsoft Excel
* **Design & Documentation:** Lucidchart, Process Definition Document (PDD)

