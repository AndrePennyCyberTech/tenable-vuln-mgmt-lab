Overview
Objective: Demonstrate vulnerability management lifecycle using Tenable.io — running unauthenticated and authenticated scans against a target host, comparing results, triaging findings by CVSS severity, and producing POA&M-style remediation documentation aligned to NIST 800-53 controls.
Tool: Tenable.io (cloud-based vulnerability management platform)
Environment: [e.g., Cyber Range — Metasploitable 2 / Windows Server target — update once confirmed]
Scan types: Unauthenticated (Basic Network Scan) + Authenticated (Credentialed Patch Audit)
Status: In Progress

NIST 800-53 Control Mapping
Control IDControl NameHow This Lab Addresses ItRA-5Vulnerability Monitoring & ScanningExecuted both unauthenticated and authenticated scans; documented findings by severityRA-5(2)Update Vulnerabilities to Be ScannedEnsured scanner plugins were up to date before running scansCA-7Continuous MonitoringDemonstrated ongoing scan cadence as part of a continuous monitoring strategySI-2Flaw RemediationTriaged Critical and High findings; mapped each to a remediation action and SLACM-6Configuration SettingsAuthenticated scan identified misconfigured services and insecure default settingsCA-5Plan of Action & MilestonesProduced POA&M tracker documenting open vulnerabilities, owners, and target remediation dates

Lab Environment Setup
Prerequisites

Tenable.io account (30-day free trial at tenable.com)
Access to cyber range target host(s)
Nessus scanner deployed and linked to Tenable.io workspace
Target host credentials (for authenticated scan)

Setup Steps

Activate Tenable.io free trial and log into console
Deploy Nessus scanner — link to Tenable.io via linking key
Confirm scanner is active and plugin feed is updated
Identify target host IP in cyber range — confirm reachability via ping
Create scan credentials (username/password or SSH key) for authenticated scan


Lab Exercises
Exercise 1 — Unauthenticated Scan (Basic Network Scan)
Objective: Identify externally visible vulnerabilities without host credentials — simulating an attacker's view or an external compliance check.
Steps taken:

Created new scan in Tenable.io using Basic Network Scan template
Set target to cyber range host IP: [target IP]
No credentials configured — unauthenticated only
Launched scan and monitored plugin execution
Exported results after scan completion

Findings summary:
SeverityCountCritical[#]High[#]Medium[#]Low[#]Info[#]
Key observations: [e.g., Open ports detected: 21, 22, 80, 445. Several services running outdated versions visible without credentials.]
Screenshot: screenshots/ex1-unauthenticated-scan-results.png

Exercise 2 — Authenticated Scan (Credentialed Patch Audit)
Objective: Run a credentialed scan to surface the full vulnerability profile of the target host — including missing patches, misconfigurations, and insecure settings not visible from the network layer.
Steps taken:

Created new scan using Credentialed Patch Audit template
Added host credentials under Scan > Credentials (SSH or Windows auth)
Set same target IP as Exercise 1
Launched scan and confirmed credential success in scan results
Exported results after completion

Findings summary:
SeverityCountCritical[#]High[#]Medium[#]Low[#]Info[#]
Key observations: [e.g., Authenticated scan returned 3x more findings than unauthenticated. Missing patches and insecure service configurations only visible with credentials.]
Screenshot: screenshots/ex2-authenticated-scan-results.png

Exercise 3 — Scan Comparison & GRC Analysis
Objective: Compare unauthenticated vs. authenticated results to demonstrate why credentialed scanning is required under federal standards — and what risk is missed without it.
Comparison table:
MetricUnauthenticatedAuthenticatedDeltaTotal findings[#][#][+#]Critical[#][#][+#]High[#][#][+#]Credential successNoYes—Missing patches visibleNoYes—Misconfig detectionPartialFull—
GRC analysis: The delta between scan types represents the true risk gap when organizations rely solely on unauthenticated scanning. NIST RA-5 and FedRAMP vulnerability scanning requirements mandate credentialed scans precisely because network-layer scanning does not surface patch status or host-level misconfigurations.
Screenshot: screenshots/ex3-scan-comparison-dashboard.png

Exercise 4 — CVSS Triage & POA&M Documentation
Objective: Triage authenticated scan findings by CVSS score and produce a POA&M-style remediation tracker — the core GRC deliverable from any vulnerability management program.
Steps taken:

Exported authenticated scan results to CSV
Sorted findings by CVSS score — filtered to Critical and High
Researched top 5 findings: CVE ID, affected component, recommended fix
Built POA&M tracker with remediation SLAs by severity (see docs/)
Documented each finding with: weakness, detection date, responsible party, target completion date

Remediation SLA applied:
SeverityRequired Remediation WindowCritical15 daysHigh30 daysMedium90 daysLow180 days
SLA based on NIST SP 800-40 and common federal agency patch management policy.
Screenshot: screenshots/ex4-poam-tracker.png

Key Findings

Authenticated scan returned significantly more findings than unauthenticated — confirming the necessity of credentialed scanning under RA-5
[Finding 2 — e.g., X Critical CVEs identified, all related to unpatched services]
[Finding 3 — e.g., Default credentials / insecure configurations detected only via authenticated scan]
[Finding 4 — e.g., Several findings mapped directly to known DISA STIG checklist items]


GRC Takeaways

Credentialed scanning is a compliance requirement, not optional — NIST RA-5(5) and FedRAMP scanning requirements explicitly call for authenticated scans to surface patch and configuration status
The POA&M is the GRC output — raw scan results have no compliance value until triaged, documented, and tracked against remediation SLAs
CVSS scores alone don't drive prioritization — asset criticality, exploitability, and remediation feasibility all factor into real-world risk decisions
Continuous monitoring cadence matters — a one-time scan is a point-in-time snapshot; NIST CA-7 requires ongoing scanning as part of an authorized system's monitoring strategy


Artifacts & Documentation
FileDescriptiondocs/lab-writeup.mdFull narrative write-up with analysis and lessons learneddocs/poam-tracker.xlsxPOA&M remediation tracker — Critical and High findingsdocs/scan-comparison.mdSide-by-side analysis of unauthenticated vs. authenticated resultsscreenshots/Evidence screenshots from each exercise

Tools & Technologies

Platform: Tenable.io (cloud vulnerability management console)
Scanner: Nessus (linked to Tenable.io workspace)
Target environment: Cyber Range — [update with target OS/type]
Frameworks: NIST SP 800-53 Rev 5, NIST SP 800-40, FedRAMP vulnerability scanning requirements


References

NIST SP 800-53 Rev 5 — RA-5 Vulnerability Monitoring
NIST SP 800-40 Rev 4 — Patch Management
FedRAMP Vulnerability Scanning Requirements
Tenable.io Documentation
DISA STIG Library


About
This lab is part of the AmpCyberTech GRC Lab Series — hands-on exercises demonstrating practical application of federal cybersecurity frameworks including NIST 800-53, FISMA, FedRAMP, and DISA STIGs.
Andre | Founder, AmpCyberTech | GRC & Compliance Analyst
LinkedIn · GitHub
