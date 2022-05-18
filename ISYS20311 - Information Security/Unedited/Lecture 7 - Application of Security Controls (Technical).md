#isys20311-infosec/lecture-7 
# Application of Security Controls (Technical)

## Types of Control

Controls seek to reduce risk to within an organisation's level of [[Lecture 6 - Risk Assessment#Risk Appetite|risk appetite]]. Types of control have been broadly defined in [[Lecture 4 - Information Security Management System#Controls|Topic 4]], but this lecture aims to go more in-depth on [[Lecture 4 - Information Security Management System#Technical Controls|technical controls]].

Controls may attempt to mitigate risks in the following ways:
- Prevent
- Correct
- Detect
- Compensate

## Network Management

To manage a network, knowledge of **[[Lecture 5 - Assets|Assets]]** (both physical and logical), **[[Lecture 5, 6 - Corporate Architecture|Architecture]]** (including systems integration and interconnectivity), and **[[Lecture 6 - Risk Assessment|Risk]]** (Including [[Lecture 6 - Risk Assessment#Identifying Vulnerabilities and Threats|vulnerabilities and threats]] alongside potential impact of a breach) are required, in order to implement **countermeasures** - i.e. the controls that need be applied.

## Attack Surface

This refers to the **sum of all potential exposures of any given system** and is affected by the following:

- Increasing number of users.
- Increasing *variety* of users.
- Growth in vulnerabilities per user, per use.
- Increased interconnectivity resulting in cascading failures.

A fair assumption can be made that attack surface and breaches are heavily correlated; security controls reduce the size of the attack surface, and thus reduce exposure and the risk of a breach.

## Technical Controls

It is required to understand specific attacks or domain-level problems in order to identify suitable technical controls, but a number of threats will require a mix of applied controls from each of the three types. Technical controls can be loosely categorised as working against two types of attacks; host-based and network attacks.

### Host-Based Attacks/Controls

These are attacks ran against a specific system or machine, such as a laptop or a desktop. They aim to compromise the host itself and the information contained within it, and this may give further access to other host machines depending on network configuration.

This type of attack is particularly concerning to large organisations, as their security is only as strong as their weakest link - and they may have potentially thousands of hosts that provide many potentially unpatched systems.

#### Host-Based Controls

There are several:

- Evidently, anti-virus software; but maintenance of it is a reactive process - attacks need to happen before our library has a signature of the malicious software.
- Host-based intrustion systems, which can monitor application-level calls to ensure they are proper.
	- For example, a properly configured system could detect if spreadsheet software is attempting to access a password directory.
- Personal firewalls exist at the network and application level.

Ideally, all of these would be combined with other types of control - such as training to promote security conscious behaviour, or system hardening/patch management policies.

### Network Attacks/Controls

These are the primary vector for attacks, being remotely executable in nature. They involve utilising existing infrastructure to threaten an asset from a geographically diverse starting point. They can include, but are not limited to:

- Denial of Service
- Eavesdropping
- Hacking/unauthorised access
- Database/web attacks

## Technical Controls (cont.)

To provide an extensive (but not exhaustive) list:

- Firewalls can prevent malicious traffic from entering the network through a maintained list of barred sources.
- Intrustion detection systems can monitor traffic for events by either generating logs (passive) or taking action (active) dependent on implementation.
- Ingress/egress filtering:
	- Ingress filters incoming packets by checking that they are from the sources they claim to be (**spoofing protection**).
	- Egress filters monitor outgoing packets to prevent malicious traffic from leaving the network.
- Network partitioning keeps key resources seperate.
- Network logs act as a detective control to assess network events.
- Authorisation and Authentication procedures make sure that parties are who they claim to be, and that they have access to the resources they request - many common methods have pitfalls in this regard.
- Encryption makes traffic between two parties secret; encrypts data stores, and can be used to offer authentication protocols and non-repudiation when using asymmetric encryption standards. They can also be used to check the integrity of data.
- K-anonymity is a procedure that involves the 'blurring' of data that can be used to identify individuals in large datasets - for example, using ranges of age instead of specific values.
	- This can limit the usefulness of a dataset in some cases, however.

### Other controls

Some controls blur the line in regards to where they are categorised. For example:

##### Access Controls

These define roles (which could be procedural) but are implemented in a technical manner. They provide a preventative measure of security control - only certain parties can access certain assets, and are prevented from accessing others.

There are broadly 3 different types of Access Control:
- Discretionary access control (DAC)
	- Individual user-based access control, based on discretion of owner.
- Mandatory Access Control (MAC)
	- Users only have access to resources that match their level of clearance.
		- Typically used in highly sensitive areas working with classified data.
- Role-based Access Control (RBAC)
	- Users have different roles that have operations and tasks associated with them.

## Summary of Technical Controls

Technical controls can be broadly summarised into the following categories, from 27001:

- Logging and Monitoring
- Workstation Security, including:
	- Host-based access control
	- Session timeouts
	- Patch management
	-  These are referred to as security requirements in the 27001 standard.
-  Communication security
-  Application lifecycle security, including:
	-  Patch management and maintenance
-  Access Control implementations

## Following Implementation

It is important to realise that selection and implementation of a potential control is not the end of the process; a *following implementation review* for the purposes of assessing effectiveness is required. Constant maintenance and appropriate updates neeed to be consistently applied in order to ensure that systems adapt to the threat landscape in an ongoing manner. For example, an estimated 200,000 systems are still vulnerable to OpenSSL's *Heartbleed* vulnerability, as it requires a patch to address.

## Vulnerability Analysis & Penetration Testing

A broad knowledge of attacks and potential vectors is a good start, but the enterprise attack surface must also be understood in detail. Companies often employ pentesters to access an organisation for potential vulnerabilities, and this may include all aspects of potential attacks; from social engineering to network attacks.

The scope of a test needs to be defined before beginning.

