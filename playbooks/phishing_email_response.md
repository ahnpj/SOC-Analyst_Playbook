🔍 Overview
Respond to a suspected phishing email reported by an end-user or detected by an email security gateway.

🚨 Trigger
User-reported suspicious email (via phishing button or ticket)

Alert from secure email gateway (e.g., Proofpoint, Microsoft Defender)

Suspicious email detected in SIEM (e.g., keyword or IOC match)

🧭 Step-by-Step Response
1. Initial Triage
Task	Tool/Platform	Notes
Confirm email source	Email headers analysis	Use tools like mxtoolbox or header analyzer
Check for attachments/URLs	Sandbox or URL scanner	Use tools like Joe Sandbox, VirusTotal, AnyRun
Identify recipients	Email gateway logs, O365	Determine blast radius

2. Containment
Task	Tool/Platform	Notes
Quarantine email	Email security platform	Search and remove using message trace
Block malicious IOCs	Firewall/Proxy/SIEM	Add to blocklists in EDR or FW rules
Alert affected users	Internal comms, IT Helpdesk	Share educational awareness if needed

3. Investigation
Task	Tool/Platform	Notes
Search for lateral movement	SIEM (Splunk/QRadar)	Correlate user login attempts post-click
Scan endpoints	EDR (CrowdStrike, etc)	Check for malware persistence
Extract IOCs	Email + sandbox reports	Store in case notes and update detection

4. Eradication & Recovery
Remove any malicious files found

Ensure no persistence mechanisms (scheduled tasks, registry keys, etc.)

Reset credentials if account compromise is suspected

5. Post-Incident
Task	Description
Report to threat intel team	Share new IOCs, sender domains, etc.
Update detection rules	Add SIEM or email detection logic
Document in IR tracker	Include timeline, findings, remediation
Conduct user awareness	Targeted training for affected users

📊 Metrics & KPIs
Time to detect (TTD)

Time to contain (TTC)

Number of affected users

Recurrence of similar phishing types

📚 References
MITRE ATT&CK T1566.001 (Phishing via Email)

NIST SP 800-61 Rev. 2 (Computer Security Incident Handling Guide)

You can create similar markdown playbooks for other common incidents like:

malware_infection_response.md

brute_force_attack_response.md

data_exfiltration_detection.md

insider_threat_investigation.md

🧰 tools_and_references/detection_queries.md (snippet)
sql
Copy
Edit
-- Suspicious Email Subject (in Office365)
DeviceEvents
| where ActionType == "MailReceived"
| where Subject has "invoice" and Subject has_any("urgent", "payment", "overdue")
| project Timestamp, SenderFromAddress, RecipientEmailAddress, Subject
✅ checklist_template.md
markdown
Copy
Edit
# Incident Checklist Template

- [ ] Validate alert source and category
- [ ] Review related logs in SIEM
- [ ] Identify affected host/user/account
- [ ] Contain and mitigate threat
- [ ] Document findings
- [ ] Notify stakeholders
- [ ] Close ticket with lessons learned
