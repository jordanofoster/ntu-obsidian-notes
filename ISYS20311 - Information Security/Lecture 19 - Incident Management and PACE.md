# Incident Management and PACE

## Security incident management

This refers to the process of identifying, managing, recording and analysing security threats or incidents in real time. Examples include:
- An attempted intrusion
- Successful compromise/data breach
- Policy violation

### Standard approaches

The [ISO/IEC Standard 27045](http://www.iso27001security.com/html/27035.html) outlines a five-step process, including:
1) Prepare for handling incidents.
2) Identify potential incidents through monitoring, and report all of them.
3) Assess identified incidents to determine appropriate next steps for risk mitigation.
4) Respond to the incident by containing, investigating and resolving it (based on step 3).
5) Learn and document key takeaways from every incident.

### Preparing for incidents - best practices

- Develop a security incident management plan and supporting policies that include how incidents are detected, reported, assessed and responded to. Have a checklist ready for a set of actions based on threat. Continuously update management procedures as necessary, particularly using lessons learned from prior incident.
- Establish an incident response team (sometimes called CSIRT) that includes clearly defined roles/responsibilities. The CSIRT should include functional roles within IT/Security as well as representation for other departments (such as legal/communications/finance/business management or operations).
- Develop comprehensive training programs for every activity necessary within the set of managemnt procedures. Practice the plan with test scenarios on a consistent basis, making refinements where needed.
- After any incident, perform post-incident analysis to learn from successes/failures and make adjustments to the security program and incident management process where needed.

### Assessing the effects

This depends on the incident, but generally:
- What files/databases are accessed?
	- Do download logs record volume of data taken?
	- Has data been published or misused?
- Any malware introduced
	- More than one antivirus toolkit may be needed.
- Websites defaced
	- Any recent backups?

#### General effects
- Theft of confidential info
- Reputational damage
	- Withdrawal of advertisers
- Business interruption
- Recovery costs
	- Increased insurance premiums
- Fines

### Report appropriately
- Regulatory requirements:
	- e.g. for GDPR, ICO must be notified of personal data breaches within 72 hours.
- Within organisation:
	- Chief Information Officer
	- Head of IT Security
	- Any reporting defined in policy?
- Others
	- National Cyber Security Centre, Action Fraud
- What do you report?
	- As rule of thumb - facts about what the *organisation* has suffered
	- Do not name individuals - can prejudice later investigation

### Contain the incident
- Limit extent of attacks
- Prevent recurrence of attack
- Assess intent of attack
- Limit effect of attack

#### Limit extent of attack
- Changing filtering rules on firewalls/routers
- Disabling known vulnerable services, such as file transfer/calendar services
- Shut down systems
- 

