Automated ServiceNow SAR Approvals (A360)

Project Summary

Developed an Automation Anywhere A360 task bot to automate manual Service Access Request (SAR) approvals in ServiceNow. The bot monitors a shared Outlook inbox for unread requests, extracts key details from the email body, and automatically completes the approval step.

Upon successful approval by the bot, ServiceNow triggers downstream provisioning of the user into the relevant Active Directory (AD) groups.

Because standard web recorders struggled with ServiceNow’s dynamic UI elements, I designed a front-end workaround using simulated keystrokes to navigate the pages. To keep the process traceable, the bot logs each transaction to an Excel spreadsheet and archives processed emails to prevent duplicate runs.
________________________________________
Key Technical Achievements

• Targeted Data Extraction: Built string-parsing logic to scrape unique identifiers (sys_id), user names, profiles, and assignment links from incoming emails.

• UI Automation Workaround: Solved object-cloning failures on dynamic ServiceNow pages by scripting a keystroke-driven navigation flow to consistently click the approval buttons.

• Audit Logging & Queue Cleanup: Programmed the bot to update a local Excel audit sheet with timestamps and transaction details, then archive processed emails in Outlook.

• Error Handling: Implemented structured Try/Catch blocks with browser-refresh commands and deliberate delays to prevent the bot from breaking during slow network loads or page timeouts.
________________________________________
Results & Impact

• Zero Manual Steps: Handed the repetitive task of reading, opening, and clicking “Approve” on SAR tickets completely over to the bot, which automatically kicks off downstream AD group provisioning.

• Faster Turnaround: Reduced the approval queue processing time from minutes per ticket to seconds.

• Reliable Tracking: Created an automated local Excel audit trail that updates in real time with every successful approval.
________________________________________
Future Considerations & Roadmap

1.	Automating Offboarding & Deprovisioning (“Remove Access” Requests)
   
• The Goal: Update the email parsing loop to handle dynamic employee lifecycle events by detecting the “Remove Access” action.

• The Execution: Add an If/Else condition inside the loop. If $sAction$ is parsed as “Remove Access,” the bot will run an alternative keystroke sequence to change the ServiceNow state dropdown to “No Longer Required,” automating the deprovisioning process.

2.	Safeguarding Admin Accounts (CMS Security Exception Routing)
   
• The Goal: Ensure highly sensitive, administrative-level access requests for Content Management System (CMS) applications are never handled automatically by the bot.

• The Execution: Introduce a verification check right after string parsing. If the $sSARProfile$ contains “Admin” or matches privileged credentials, the bot will skip automatic processing, flag the ticket as an exception, and send a direct email follow-up to the CMS SAR Handler for manual vetting.

3.	Resilient Error Recovery (System Exceptions)
   
• The Goal: Prevent the automation from silently failing during network lag or loading errors on the ServiceNow UI.

• The Execution: Expand the global Catch block. If the bot fails to complete an approval due to a browser timeout, it will capture the exact error message and automatically email the original SAR Approver to step in and handle it manually.


