# Risk Assessment

## Holistic Risk Management

Focus on risk management tends to be towards applications, devices, viruses, hacking and other technical issues - but this is not the entirety of the issue, as security chiefly manifests as a business issue as well. Standards define *three* tiers to risk management:

- Organisational tier
	- Risk to the business as a whole.
- Business tier
	- Risk to major organisational functions, such as defining criticality of information flows between org and customers.
- Information Systems tier
	- Risks from an IS perspective, where the focus of this module is.  

### Levels of Risk

Inherent Risk refers to the exposure from a specific risk without controls applied. *Current Risk* is the current potential that a vulnerability will be exploited, given that controls are in place. 

*Residual Risk* is the level of risk remaining after action has been taken (i.e. following risk assessment exercises and implementation of the ensuing security plan), and *Risk Appetite* refers to the level of risk that we are prepared to accept/tolerate/be exposed to, and is set at the organisation tier.

#### Risk Appetite
![[RiskAppetite.png]]
The goal is to get our level of residual risk for any one threat to less than the pre-determined level defined by the appetite itself.

### Risk Management Lifecycle
![[RiskMgmtLifecycle.png]]

#### The Process
- Risk Identification
	- Finding, recognizing and describing risks.
- Risk Analysis
	- Comprehending thne nature of the risk and determining risk levels involved (likelihood and impact).
- Impact
	- Amount of harm caused when threats reach an asset; evaluated against CIA.
- Likelihood
	- The chance of the threat occuring.
- Risk Evaluation
	- What the ultimate decision is based on the results from the analysis phase.

##### Risk Identification

Involves Asset Identification, as covered previously, and identifying threats to those assets; which is often much more difficult than it seems (Kemuri Water Company incident). RI also involves understanding how assets work together, and how they work within an organisational context - all in order to identify vulnerabilities to those assets.

###### Understanding Vulnerabilities

Vulnerabilities can be broadly summarised as occuring due to the following:
- Flaws, or unintended functionality.
- Features - intended functionality that can be misused.
- User Error, originating from human mistakes.

###### Flaws

Flaws may be a result of poor design or mistakes made during implementation. For example, 0-day exploits are often introduced during system updates. There is a huge market trading in such exploits that have been discovered as a result of reverse engineering implementations; a number of organisations maintain common vulnerabilities that are worth keeping an eye on:

- CVE (Common Vulnerabilities  and Exposures)
- NVD (US National Vulnerability Database)

###### Features

Features refer to intended functionality that can be misused by an attacker. For example, the use of macros is still extremely common as an attack vectors. such as BlackEnergy, which used Excel macros delivered through spear phishing attacks to launch itself. Javascript also provides a common means of attack through Cross-Site-Scripting (XSS).

###### Human Error

Human Error is a significant source of vulnerabilities, and can either be accidental or intentional; it can include being persuaded to install malicious software or forgetting to set strong password policies, or errors that arise from human interaction, such as accidental or intentional action that disrupt productivity, such as working on a production server instead of development.

###### Identifying Vulnerabilities and Threats

Examples include:

| Threat Agent | Can Exploit This Vulnerability; | Resulting in this Threat: |
| ------------ | ------------------------------- | ------------------------- |
| Malware | Lack of anti-virus software | Virus infection |
| Hacker | Power services running on a server | Unauthorised access to confidential information |
| Users | Misconfigured parameters in the OS | System Malfunction |
| Employee | Lack of training or standards enforcement, lack of auditing | Sharing mission critical information, Altering data inputs and ouputs from data process applications |
| Contractor | Lax access control mechanism | Stealing trade secrets |
| Attacker | Poorly written application, Lack of stringent firewall settings | Conducting a buffer overflow attack, Conducting a DoS attack |
| Intruder | Lack of security guard | Steal physical artefacts |


##### Risk Analysis Approaches

###### Quantitative Approach

This involves assigning monetary and numeric values to all elements of the process, and forming an equation to determine total and residual risk; a common example is:

Asset Value $\times$ Exposure Factor $= SLE$ (Single Loss Expectancy)

Exposure Factor represents the % of loss if the threat occured (i.e. if a server costs £150,000 and 25% of the asset is damaged upon threat realisation). Calculating the SLE of the server would then follow as such:

$SLE = 150000 \times 0.25 = £37,500$

There is also this equation:

Annual Loss Expectancy (ALE) $=$ SLE $\times$ Annualised Rate of Occurance (ALO)

###### Outcomes of Quantitative Approaches

Risk analysis has clearly defined goals and will generally lead to the following outcomes:
- Monetary values assigned to assets
- Comprehensive list of all possible and significant threats
- Probability of occurence rate of each threat
- Loss potential the company can endure per threat
- Recommended controls

Despite the level of justification and background work that goes into this, there is still a degree of subjectivity, including degrees of uncertainty (such as how to calculate ALO).

###### Qualitiative 

This is a softer approach that assigns ratings to risks in order of high, medium, low, and categorising responses based on these ratings. The process required invovles best judgement, practices, and much experiences, but in lieu of this, extensive data gathering exercises should take place with asset owners and staff familiar with involved business processes.

##### Which Method?

Experienced gap analysts will be able to produce roughly the same outcome using the qualitative approach, but this requires years of experience. The difficulty with the quantitative method involves getting hold of the values and levels of uncertainty that are involved - it is time consuming and expensive to implement, but will give authenticity to recommendations, as senior management understand numbers and costings more...

##### Formal Methods of Risk Analysis

- NIST risk management; mainly focused on IT security issues and does not explicitly cover larger threat types, such as how security risks are associated with business risks.
- Facilitated Risk Analysis Process (FRAP) 
	- Focus only on assets that need the most attention and are intended to be used on one process at a time (i.e. low level)
- Operationally Critical Threat, Asset and Vulnerability Evaluation (OCTAVE)
	- People focused, requiring data gathering exercises with those familiar with the organisation.
- Failure Modes and Effect Analysis (FMEA)
	- Mainly used in production environment through failure analysis understand cause and effect.

###### Example Risk Register

There are multiple methods of generating a risk register; one such template could be shown below:

| ID | Risk | Vulnerability | Impact | L | Risk Level | Action | Control | Cost | Plan |
| -- | ---- | ------------- | ------ | - | ---------- | ------ | ------- | ---- | ---- |

Risk registers are required to comply with international standards such as the Turnbull report and Sarbanes-Oxley, both of which came into play as a result of major corporate incidents.