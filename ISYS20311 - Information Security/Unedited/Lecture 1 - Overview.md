#isys20311-infosec/lecture-1 
# Overview

## Information Security Principles

### CIA Triad
- The CIA Triad represents three principles that inform **information security stratagem** amongst organisations. 
- Assessments are undergone to examine whether these tenets have been compromised.
- Controls put in place aim to preserve this triad across all affectable assets.

![[CIA.png]]

#### Confidentiality

ISO27001 defines confidentiality as *"The property that information is not made available or disclosed to unauthorised individuals, entities or process."* Enforcement of confidentiality is done through the need-to-know principle and attacks against this principle aim to gain knowledge somehow, through various means:

- Packet sniffing
- Password attacks
- Keyloggers
- Social engineering

#### Integrity

ISO27001 defines integrity as *"The property of safeguarding the accuracy and completeness of assets."* This is important as information is only useful to a company (or by extension, anyone at all) if it accurately represents what it is supposed to. Attacks against integrity aim to keep trust in the system, but exfiltrate and/or modify information to mislead others; examples include:

- Session hijacking
- man-in-the-middle (**MITM**) attacks.

#### Availability
ISO27001 defines availability as *"The property of being accessible and usable upon demand by an authorised entity.* It should be noted that unavailable information does not act as information at all - rather, it becomes irrelevant as it cannot be given context. If compromised, restoring availability can be one of the most expensive endeavours for a company, costing millions. Examples of attacks against availability include:

- Denial of Service (**DoS**) attacks
- Physical tampering of devices to restrict access
	- Erasing/destroying storage devices,
	- Encrypting data...
	- ...and modifying file permissions, amongst other things.

### Non-triad principles

These principles are not included as part of the CIA triad, but are similarly important:

#### Accountability & Non-Repudiation

Accountability represents the knowledge of which individuals are responsible for which parts of a system. Non-repudiation refers to the inability for a party to deny accountability for an action.

##### Authentication & Authorisation

Both of these procedures can be used to enforce the above principles. **Authentication** refers to the process of **determining who somebody is.** this can be done through various factors:

- Something you are (**biometrics**)
- Something you have (**Smartcard/Security Key**)
- Something you know (**Credentials e.g. Username & Password**)
- Somewhere/when you are (**Location/Timezone checks**)

**Authorisation** refers to the process of determining if somebody is allowed access to something, typically confirmed through authentication.

### Assets

Assets are anything that is **considered valuable to an organisation.** This is **not neccessarily measured monetarily** - for example, businesses also value things such as reputation and consumer trust. They can, however, be mostly consolidated into three main types:

- Pure information
- Physical items
- Software used to process information

#### Threats

Threats are anything that could **cause damage to an asset,** and are typically described as **the cause of an incident.** This usually refers to technical attacks such as hacking, but all potential threats to assets are considered as part of INFOSEC regardless. [The Buncefield fuel depot explosion in  2005](https://en.wikipedia.org/wiki/Buncefield_fire) shows why non-technical threats still require consideration.

##### Vulnerabilities

Vulnerabilities are weaknesses that **increase the chance of a threat.** To provide an example; **fire** is a threat because it **endangers physical assets.** making the decision to place a data centre next to a fuel depot makes the **data centre vulnerable because it is more likely to be threatened by a fire hazard.**

#### Risks
Risks are considered to be **potential events** that would **damage an asset.** They have **two key attributes:**
- **Likelihood that the risk will occur**
- **Impact of the risk on the asset.**

##### Controlling Risks
Risks can be controlled to an 'acceptable' level through the following methods:
- **Reducing/Removing vulnerabilities**
- **Anticipating and preparing for risks**
- **Insuring at-risk assets**

It should be noted that chances of risk can **rarely be reduced to zero without removing the asset itself.** As such, risk mitigation often becomes a balancing act within the scope of what a company can afford to lose.