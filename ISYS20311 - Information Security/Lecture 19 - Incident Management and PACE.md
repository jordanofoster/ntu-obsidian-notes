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
- Disconnect systems from network
- Call in experts if necessary


#### Prevent recurrence of attack
- Identify and close the gateway
	- Change all passwords just in case
- Scan all machines for undetected infection
	- Remove any found malware

#### Assess attack intent
- Set traps
	- Honeypot servers
	- Files/directories with attractive names
- Assess actions
	- Reconnaissance?
	- Denial of Service?
	- Blackmail?
	- Who/what was targeted?

#### Limit effects of attack
- Possibilties:
	- Proactive admission
		- Tell world before hacker does
		- Tell world about mitigative measures
	- Restore backups
		- Assuming they've been made (...right?)
	- Pay blackmail?
		- Official sources always say no, but they don't suffer from lost data
		- No guarantees blackmailers will keep their side of the bargain or not raise the asking price
		- Beware of middlemen

## Collect Evidence
This must be court admissible, which sometimes slows down procedure and weighs against business continuity. Computer forensics may be required, in which case the following should be followed:

- Do not switch off turned on machines
- Only turn off machines if they are running destructive code
- If machines are on, remove the network cable and/or disable the wifi (preferably while being video recorded)
- If police are involved, an affected computer may be lost for months:
	- Get a forensic specialist to take an image of the computer for analysis

## Potential prosecution/civil action
If perpetrators are identified, what should they be charged with? English law distinguishes criminal offences and civil offences:
- The Crown Prosecution Service decides who is charged with a criminal offence
- The offended party decides who is sued for a civil offence

### Police and Criminal Evidence Act 1984 (PACE)
This regulates what police forces can and cannot do. Codes of practice cover:
- Stop and search
- Arrests
- Detention
- Investigation
- Identification
- Interviewing detainees

This affects the following aspects of cybersec incidents/investigations:
- Disclosure of information
- Admissibility
- Retention

#### Disclosure of information under PACE

Schedule 1 of PACE allows a court to make an order that an organisation must disclose specific information that would otherwise be legally confidential to the court.

Schedule 2 of Part 1 states the following: Organisations may choose to disclose personal data to the police for the purpose of investigating, detecting and preventing crime. It is not mandatory, but the organisation is responsible to ensure that risk of harm from non-disclosure is lower than the breach of privacy disclosure causes.

Similar laws state:
- It is a criminal offence to not disclose phone/other passwords to the police if a court order has been obtained under section 49 of the Regulation of Investigatory Powers Act (RIPA)
- Section 7 of Terrorism Act 2000 can be used to compel disclosure of passwords at ports/airports.

### Admissibility of evidence

PACE has a lot to say regarding evidence admissibility:
- Hearsay
- Confessions
- Bad character

For cybersecurity, only *Hearsay* is relevant: normally, evidence from 'a friend of a friend' is non-admissible, as witnesses must have observed it directly. However, it is very rare to observe someone using a computer to commit an offence, and far more common to discover evidence of such on the computer itself.

Thus, special rules are needed to make computer evidence admissible. The first attempt was the Civil Evidence Act 1968, which included some conditions that were difficult to prove, such as:

*"Throughout the material part of the period, the computer was operating properly."*

#### Admissibility of evidence under PACE
PACE loosens the "operating properly" statement:

*"In any proceedings, a statement contained in a document produced by a computer shall not be admissible in evidence of any fact stated therein unless it is shown - (a) that there are no reasonable grounds for believing that the statement is inaccurate because of improper use of any computer; (b) that at all material times the computer was operating properly, or if not, that any respect in which it was not operating properly or was out of operation was not such as to affect the production of the document or the accuracy of its contents."*

However "improper use" covers any use of the computer by anyone after the suspect last used it - so forensic computing procedures are carefully designed to avoid that.

#### Other relevant acts of admissibility

- Youth Justice and Criminal Evidence Act 1999
	- This loosened the "operating properly" requirement further still; now computers are assumed to have been functioning properly unless evidence to the contra
