# Information Security Management System

## Information Assurance
Refers to *the confidence that information systems will protect the information they carry and will function as they need to, when they need to, under the control of legitimate users* according to the UK cabinet office. An information system in this regard is **not  necessarily technical** - they can also be a series of policies, training programs and documentation alongside technical implementations for the entire organisation.

## The Information Security Management System (ISMS)

The ISMS preserves the CIA triad around information by applying risk-management processes, thereby giving confidence to invested parties that the risks have been adequately managed.

To do so, an ISMS must be integrated within the organisation's processes and management structure - and information security as a whole must be considered through the entire design, including processes, information systems and controls.

To simplify, an ISMS is more or less a guidebook to information assurance within an organisation.

### Parts of an ISMS

| System Component | Purpose/Detail |
| -----------------	| -------------- |
| Context |	The basis for what needs to be done |				 
| Scope | Defining what is to be protected/supported |
| Objectives | The basis for evaluation of overall effectiveness |
| Policy | Assurance and directive to the organisation |
| Planning | Aligning objectives with components, managing programme |
| **Risk assessment (analysis) & treatment** | **Analysis of what risks exist to which assets, which are acceptable and what controls are needed** |
| Statement of Applicability | 'Checklist' (have likely controls been considered?) |
| Assurance process | Internal audits, management reviews, performance improvements, non-conformance & continual improvement |

#### Scope

Scope is ideally present throughout every level of an organisation, but in practice, some of it is limited to sensitive parts of the organisation itself. This again is due to the required balancing act of security vs usability.

#### Policy

A *policy* is a high-level statement of security goals for an organisation. they should be short and to the point to make implementation more likely (no-one will implement a policy 100s of pages long and will inevitably take shortcuts.)

#### Risk Analysis

This is the process of identifying assets, vulnerabilities and the likelihood of exploitations in regard to violating the CIA triad. This is typically combined with an analysis of impact in event of compromise, in order to identify whether it is worth applying controls to protect an asset, and if so, which should be implemented. Such proceedures are a key part of IS management.

##### Outcomes of Risk Analysis

- Asset registers, a list of all points of concern, and who has ownership of what.
- Risk registers, which are a list of all identified risks and potential mitigating controls that can be used to address them.

##### Controls

Controls are put into place to mitigate risk to acceptable levels. They can be broadly categorised into 4 subtypes:

- Technical
- Procedural
- Physical
- Managerial controls are sometimes (but rarely) used, and are not covered here.

And controls are further defined as being either *Preventative, Detective or Corrective.* It should be noted that risk cannot be completely removed, and controls merely exist to make a risk of compromise more palatable to the company.

###### Technical Controls

These, as the namesake suggests, use technology as a basis to minimise risks. These include methods such as:

- Access control
- Encryption
- Anti-virus software
- Intrustion Detection Systems, Firewalls, etc.

###### Procedural/Administrative Controls

These are procedures and policies placed to define behaviour within the organisation itself, such as:

- Password use policies (such as *password aging*)
- Training programs
- Recruitment policies (Not hiring those with a *criminal record,* for example)
- Fair usage policies, Bring Your Own Device guidance, away-from-desk policies, etc.

###### Physical Controls

These refer to structural security measures to deter and/or prevent physical access to assets, such as:

- CCTV cameras
- Alarm systems
- Staff cards
- Biometrics, etc.

#### Planning
##### The Security Plan
Security plans should set out the following:

- Policy - the goals of the effort being made.
- State of the current ISMS and security effort in the organisation.
- Requirements needed to meet recomended security goals through risk assessments.
- Recommended controls to address vulnerabilities
- Defining those accountable for each stage of the process and individual assets.
- Timetable that defines deployment timescale
- Defined Incident Response Procedures in event of breach
- Continuing attention, defined in how often additional review should be done.

###### Information Security Lifecycle

![[InfoSecLifecycle.png]]

#### Incident Response

Regardless of how much we reduce risk, attacks - and breaches - still happen. As such, staff require training to be able to identify potential incidents, and what to do when having seen one.

Following an incident, responses typically include 5 phases:
- Reporting
	- Typically from detective controls monitored by staff (i.e. network logs)
- Investigation
- Assessment
- Corrective Action
- Review

##### Incident Response Planning

When planning an incident response procedure, some of the following things must be considered:

- Is there actually a team in place to handle things?
	- And if an IRT does actually exist, we should make sure it contains a cross section of the organisation, to create sufficient breadth of knowledge to deal with situations.
- Plans need to be clear - how is evidence recorded? Are we following procedures outlined in the *Police and Criminal Evidence Act 1984?* if not, we could struggle to prosecute.

##### Business Continuity Planning

This involves ensuring business operations continue following significant incidents or disasters. It typically involves defining 'essential' assets, with the following criteria:

- What key assets need to be 'online' to achieve business objectives?
- How long can our business operate without key assets and maintain financial viability?
	- This is typically assessed via a Business Impact Analysis done alongside risk assessments.

Exercises are often implemented in order to test the readiness of written plans.

##### Disaster Recovery Phase

This refers to the period of time required before returning to maximum service level. It involves questions and scenarios as shown below:

- What the Recovery Time Objective is (how long can an organisation survive without affected assets.)
- What the Recovery Point Objective is (what point in time systems should be restored.)
	- This is typically less that RTO, to account for complications.

Sometimes, full disaster recovery is impossible; plans used during the disaster period may become permanent and a part of normal operating procedure.

### Key Roles in the ISMS

Various roles are spread across an organisation - assurance activities are always written into every member's role as part of the ISMS.

#### Chief Information Security Officer (CISO)
The CISO is responsible for the day-to-day running of information assurance policies.
Occasionally, this role is at board level to assure responsibility/accountability to shareholders and encourage top-down assurance culture - but if not, someone at board level must always take ownership of the ISMS, even if they are not neccessarily the CISO themselves.

