#isys20311-infosec/lecture-9
# Certification Standards

These are national or international standards for information security that organisations can be certified as having met. This gives them and others confidence that they operate good information security practices.

Although certification does not require that organisations never suffer a cyber attack, if they do and the reason for said attack is resultant of a failure to follow certified practice, the organisation is at risk of losing their certification.

## Why is certification good for an organisation?

### Complying with legal requirements

Legal requirements are to be discussed in a later lecture.

Most legal requirements can be resolved by following policies that meet a standard.

### Achieving marketing advantages

If a company is certified and its competitors are not, your products/services become more enticing to potential customers.

### Lower costs

The main philosophy of security standards is to prevent security incidents from happening in the first place, thereby lessening costs required to recover after one.

### Better organization within the company

Often, employees do not know what needs to be done when and by who. Standards encourage companies to write down their main processes instead, helping remedy this issue.

## Well-Known Standards

- **ISO 27001,** granted by the International Standards Organisation.
- **NIST Cybersecurity Framework,** granted by the US National Institute of Standards and Technology.
- **IASME Governance,** which is the UK standard for SMEs, and is a form of ISO27001 with reduced complexity. Businesses that follow it get free cybersecurity insurance.
- **US FFICE Cyber Security Assessment Tool,** mandated for regulated US banking organisations.
- **Payment Card Industry Data Security Standard,** mandated by most brands of credit card.

### ISO/IEC 27001

This is an international standard published by the International Standardization Organisation (ISO). It describes how to manage INFOSEC within a company, with its main philosophy being to manage risks - by finding out where they are, and then systematically treating them.

The safeguards and controls implemented as part of ISO 27001 are usually in the form of policies, procedures and technical implementation, such as software and equipment.

#### Sections

ISO/IEC 27001 is split into 11 sections, including Annex A:
- Sections 0-3 are introductory and not mandatory for implementation; 4-10 are mandatory.
- Controls from Annex A only need to be implemented if they are declared as applicable in the Statement of Applicability.

###### Section 0: Introduction

Purpose and compatibility with other management standards.

###### Section 1: Scope

This standard is applicable to any type of organization.

###### Sections 2-3: Normative references, terms and definitions

These refer to ISO/IEC 27000.

##### Planning Phase

###### Section 4: Context of the organization

This defines requirements for understanding external/internal issues, interested parties and their requirements, and defining scope within the ISMS.

###### Section 5: Leadership

This defines top management responsibilities and other roles/responsibilities.

###### Section 6: Planning

This defines requirements for risk assessment and treatment, Statement of Applicability, risk treatment plan, and setting INFOSEC objectives.

###### Section 7: Support

This defines requirements for availability of resources, competences, awareness, communication and control of documents and records.

##### Do, Check, Act

###### Section 8: Operation

This defines the implementation of risk assessment/treatment, as well as controls and other processes needed to achieve INFOSEC objectives.

###### Section 9: Performance evaluation

This defines requirements for monitoring, measurement, analysis, evaluation, internal audit and management review.

###### Section 10: Improvement

This defines requirements for nonconformities, corrections, corrective actions and continual improvement.

###### Annex A


This annex provides a catalogue of 114 controls/safeguards placed in 14 sections (A.5-A.18).

#### Steps To Implementation: Define

1) Get support of top management
2) Use project management methodology
3) Define ISMS scope
4) Write top-level INFOSEC policy
5) Define risk assessment methodology
6) Perform risk assessment and risk treatment
7) Write Statement of Applicability
8) Write risk threatment plan
9) Define how to measure efficacy of controls and ISMS

#### Steps To Implementation: Do

10) Implement all applicable controls/procedures
11) Implement training/awareness programs
12) Perform all daily operations prescribed by ISMS documentation
13) Monitor and measure ISMS
14) Perform internal audit
15) Perform management review
16) Implement corrective actions

#### Mandatory Documentation

- Scope of the ISMS (clause 4.3)
- Information security policy and objectives (5.2/6.2)
- Risk assessment and risk treatment methodology (6.1.2)
- Statement of Applicability (6.1.3d)
- Risk treatment plan (6.1.3e & 6.2)
- Risk asssessment report (8.2)
- Definition of security roles and responsibilities (A.7.1.2/A.13.2.4)
- Inventory of assets (A.8.1.1)
- Acceptable use of assets (A.8.1.3)
- Access control policy (A.9.1.1)
- Operating procedures for IT management (A.12.1.1)
- Secure system engineering principles (A.14.2.5)
- Supplier security policy (A.15.1.1)
- Incident management procedure (A.16.1.5)
- Business continuity procedures (clause A.17.1.2)
- Statutory, regulatory, and contractual requirements (clause A.18.1.1)

#### Mandatory Records

- Records of training/skills experience/qualifications (clause 7.2)
- Monitoring and measurement results (clause 9.1)
- Internal audit program (clause 9.2)
- Results of internal audits (clause 9.2)
- Results of management review (clause 9.3)
- Results of corrective actions (clause 10.1)
- Logs of user activities/exceptions/security events (clauses A.12.4.1/A.12.4.3)

#### Related Standards

- **ISO/IEC 27002,** which defines guidelines for the implementation of the 114 controls listed as part of ISO 27001.
- **ISO/IEC 27004,** which outlines how hto measure whether an ISMS has achieved its objectives.
- **ISO/IEC 27005,** which outlines how to perform risk assessment & risk treatment;
- **ISO 22301,** defining requirements for business continuity management systems.
	- A.17 of ISO 27001 requires that business continuity be implemented.
- **ISO 9001** defines requirements for quality management systems.
	- ~25% of ISO 27001 and ISO 9001 requirements are the same; document control, internal audit, management review, corrective actions, setting the objectives, and managing competences. As a result, if a company implements ISO 9001, ISO 27001 is much easier to achieve.
	
## The Information Security Management System

In most cases, companies already have all the hardware and software necessary in place - but they are being used in an insecure manner. As a result, the majority of ISO27001's implementation is about setting the organisational rules needed in order to prevent security breaches.

The [[Lecture 4 - Information Security Management System|Information Security Management System (ISMS)]] is at the core of ISO 27001; an ISMS is a systematic approach to managing sensitive company information so that it remains secure; it includes people, processes and IT systems, managed by applying a risk management process.

## Case Study - Charityshare

Charityshare is a consortium IT venture, jointly owned by The Children's Society, Alzheimer's Society and AgeUK. Formed in November 2004, it enables the charities to share operational IT services, reduce costs through economies of scale, increase return on precious charity funds invested in IT, and guarantees not-for-profit IT provision.

The company needed to reassure their funding partners and the outside world that confidential data – including records pertaining to vulnerable individuals and payment card details – are well-protected within the organisation’s information security management system (ISMS), and that the situation will be reviewed on a regular basis.

The risk assessment process identified 114 controls as necessary. The consultant's report highlighted the document repository as an area for improvement. Later, the following was said about it:

*"With hindsight, I would say that this was the most valuable part of the service provided by the consultant as it saved a great deal of time and cost. In fact, it really paid for their consultancy fees.*

*It's not that we were doing anything wrong. Rather, he saw ways of reducing the total effort of maintaining three sets of records for each of our three partner charities, removing the duplication that was creeping in. He helped us to devise a better template and fostered our adoption of an intranet document centre that was praised by the external assessor for ISO27001."*

The key issue presented here, however, was merging the documents of 4 different companies into the documentation of one system.

The consultant also provided a *document toolkit,* a much valued source of document templates - alongside training through *management workshops* to test assumptions.

The result was that Charityshare's Statement of Applicability was fully approved by the external assessor, alongside an ISO 27001 auditor. Of note is this quote:

*"It’s vital that managers take responsibility for their areas of risk. What’s the point of evaluating a risk if there’s no-one to do what’s needed to mitigate that risk?"*

## How to get certified

### Organisations

Organisations must implement the standard as explained in previous sections, and then go through the certification audit performed by the certification body. The audit is performed in the following steps:

- Stage 1 audit (Documentation review)
	- Auditors review all documentation.
- Stage 2 audit (Main audit)
	- Auditors perform an on-site audit to check whether all activities in a company are compliant with ISO 27001 and ISMS documentation.
- Surveillance visits
	- After the certificate is issued, auditors will occasionally check during the 3-year validity period whether the company has maintained its ISMS.

### Individuals

Individuals can go for several courses in order to obtain certificates. The most popular are:

- ISO 27001 Lead Auditor Course
	- 5-day course that teaches how to perform certification audits.
		- Intended for auditors and consultants.
-  ISO 27001 Lead Implementer Course
	-  5-day course that teaches implementation of the standard.
		-  Intended for INFOSEC practitioners and consultants.
- ISO 27001 Internal Auditor Course
	- 2/3-day course that teaches basics of the standard, and how to perform an internal audit.
		- Intended for beginners in the topic and internal auditors.

 
