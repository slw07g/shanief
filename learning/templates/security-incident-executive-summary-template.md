# Executive Summary: Security Incident Report

*Template author: [Shanief Webb](https://shanief.com/about). Part of the [Security Incident Response 101](https://shanief.com/learning/incident-response/) module.*

## 1. Incident Metadata

- **Incident ID / Tracking #:** [e.g., INC-2026-XXXX]
- **Incident Title / Name:** [Short descriptive title]
- **Date & Time Discovered:** Date [HH:MM Timezone]
- **Severity Level:** [ ] Critical  [ ] High  [ ] Medium  [ ] Low
- **Current Status:** [ ] Active  [ ] Contained  [ ] Eradicated  [ ] Closed

## 2. High-Level Incident Summary & Impact

### Executive Summary Narrative

*(Provide a concise, high-level summary for executive leadership detailing the overall operational status, initial detection context, and immediate containment measures taken. Avoid detailing specific data impact, user numbers, or user experience metrics here to prevent premature reporting triggers prior to formal legal review; detailed assessment should be handled under Section 4: Breach Determination & Regulatory Assessment Exercise.)*

### Impact Assessment

- **Operational Impact:** [Describe service disruptions, operational downtime, or impacted business processes]
- **Financial Impact:** [Estimated direct costs, downtime losses, ransom demands (if applicable), or remediation expenses]
- **Systems Impact:** [List specific systems, applications, or databases affected. Record data categories and notification decisions in Section 4, not here.]
- **Reputational Impact:** [Potential or realized brand damage or public PR impact]

## 3. Incident Lifecycle Actions Taken

| Phase | Key Actions / Steps | Status / Notes |
| :--- | :--- | :--- |
| **Detection & Identification** | [SIEM alert / EDR notification triage; verified scope and initial IoCs] | [Complete / Date & Time] |
| **Containment** | [Host isolation, account disabling, credential resets, network segmentation] | [Complete / In Progress] |
| **Analysis & Investigation** | [Root cause determination, forensic analysis, threat actor attribution, TTP mapping] | [In Progress / Pending Forensics] |
| **Remediation & Eradication** | [Malware removal, patching exploited vulnerabilities, system hardening, firewall updates] | [Planned / In Progress] |
| **Recovery & Restoration** | [Phased system restoration from backups, integrity testing, enhanced monitoring deployment] | [Pending / In Progress] |
| **Post-Incident Review** | [Lessons learned session, corrective action plan assignment, policy/tooling updates] | [Scheduled] |

## 4. Breach Determination & Regulatory Assessment Exercise

*Use this section to systematically evaluate whether this security incident constitutes a data/privacy breach requiring legal, regulatory, or customer notifications.*

### Breach Determination Assessment

| Assessment Question | Details / Findings | Status |
| :--- | :--- | :--- |
| **1. Was sensitive or regulated data involved?** | [Specify PII, PHI, PCI-DSS, IP/Confidential, Credentials, or None/Unconfirmed] | [Yes / No / Unconfirmed] |
| **2. Was there evidence of unauthorized access, acquisition, or exfiltration?** | [Specify Exfiltration, Confirmed Access, Potential Access, Encrypted/Unreadable, or No Evidence] | [Yes / No / Investigating] |
| **3. Is there a reasonable likelihood of financial, physical, or reputational harm?** | [Evaluate impact to affected individuals and business] | [High / Medium / Low / None] |
| **4. Were effective compensating controls (e.g., uncompromised encryption) in place?** | [Detail encryption standards, key security, or additional safeguards] | [Yes / No / Partial] |

### Legal & Regulatory Threshold Check

*Timelines below are summaries for planning. Confirm applicability and deadlines with legal counsel against the official sources linked in each row.*

| Applicable Framework / Law | Mandatory Reporting Timeline | Trigger Condition / Notes |
| :--- | :--- | :--- |
| **GDPR** ([Art. 33 & 34, official text](https://eur-lex.europa.eu/eli/reg/2016/679/oj)) | Supervisory authority: without undue delay and, where feasible, within 72 hours of awareness.<br>Individuals: without undue delay when the breach is likely to result in high risk. | [Personal data breach, unless unlikely to result in a risk to the rights and freedoms of natural persons] |
| **SEC Form 8-K Item 1.05** ([SEC announcement](https://www.sec.gov/newsroom/press-releases/2023-139)), public companies only | 4 business days after the incident is determined to be material. Delay is permitted only if the U.S. Attorney General determines disclosure poses a substantial risk to national security or public safety. | [Material cybersecurity incident. Make the materiality determination without unreasonable delay after discovery.] |
| **HIPAA Breach Notification Rule** ([HHS guidance](https://www.hhs.gov/hipaa/for-professionals/breach-notification/index.html), [45 CFR 164.400-414](https://www.ecfr.gov/current/title-45/subtitle-A/subchapter-C/part-164/subpart-D)) | Individuals: without unreasonable delay, no later than 60 calendar days after discovery.<br>500+ individuals: notify HHS at the same time as individuals; if more than 500 residents of a state or jurisdiction, also notify prominent media within 60 days.<br>Fewer than 500: log and report to HHS within 60 days after the end of the calendar year. | [Breach of unsecured PHI. Presumed a breach unless a documented risk assessment shows a low probability of compromise.] |
| **California Civil Code § 1798.82** ([official text](https://leginfo.legislature.ca.gov/faces/codes_displaySection.xhtml?lawCode=CIV&sectionNum=1798.82)) | California residents: within 30 calendar days of discovery (effective Jan 1, 2026).<br>More than 500 California residents: submit a sample notice to the Attorney General within 15 calendar days of notifying residents. | [Unauthorized acquisition of unencrypted personal information, or encrypted data where the key was also compromised] |
| **Other U.S. state breach laws** ([NCSL state-by-state index](https://www.ncsl.org/technology-and-communication/security-breach-notification-laws)) | Varies by state. Check every state where affected individuals reside. | [Definitions of personal information, deadlines, and regulator notice thresholds differ by state] |

### Final Breach Classification & Sign-Off

**Breach Status Determination:**

- [ ] **CONFIRMED BREACH:** Meets statutory definition; formal notification protocols initiated.
- [ ] **SECURITY INCIDENT ONLY (NON-BREACH):** No sensitive data compromised or accessed.
- [ ] **UNDER LEGAL REVIEW:** Pending further forensic/legal analysis.

**Legal / Privacy Counsel Sign-Off:** Person, Date

**Next Steps / Notification Plan:** [Summary of required notifications to authorities, customers, or insurance providers]
