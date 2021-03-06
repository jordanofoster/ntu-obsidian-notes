
#isys20311-infosec/lecture-10
# GDPR: The General Data Protection Regulation

## Legal Requirements

In many countries, failure to protect customers' personal data adequately is against the law. This typically results in a fine for the organisation, but other penalties are possible.

The European Union's General Data Protection Regulation (GDPR), is an example of one such law. Because it is an EU directive, it actually generates a set of laws; every EU country is required to pass a law themselves to implement it. GDPR is recent and other new laws may copy it, and it claims to apply to anyone who does business in an EU country

## The General Data Protection Regulation

GDPR replaces the Data Protection Directive of 1995, and was enforced in member states of the EU from 25th May 2018. It creates a (fairly) level playing field across the EU.

### Changes Since 1995

- Jury opinion on data protection has changed over time due to case law, particularly regarding Campbell v MGN in 2002. 
- The average UK business now uses 24 systems to manage and store personal data; with one in five using 40. Meanwhile, almost half share personal data from customers with other businesses.
- On a daily basis, large enterprises collect data from 577 individuals, with 25% collecting data from more than 1000 people every day.
- Despite the fact that almost two-thirds storee and manage personal data based on predictive analytics, they could not agree who owns the data. A quarter think the customer is the owner, while half think it is the company.

Regarding technological advancements, we now have cloud storage, backup servers and recovery tech - and societally an increased focus on privacy.

### Who has to comply?

- Data controller/processors established in one or more EU Member State
- Data controller/processors established outside the EU, and:
	- Offering goods/services to individuals in the EU
	- Monitoring behaviour of individuals taking place in the EU
- Enforcement of GDPR outside the EU can be difficult, but preventing further business in the EU is *not* - so this will still apply to many or all UK businesses in the UK after Brexit.

### Key Roles

- Data subject
- Data Controller
- Data Processor
- Data Protection Officer
- Supervisory authorities

### Principles and Accountability

#### Principles

- Lawfulness, fairness and transparency
- Purpose limitation
- Data minimisation
- Accuracy
- Storage limitation
- Integrity and confidentiality

#### Accountability

- Compliant policies and procedures
- Records of processing
- DPO appointment
	- Mandatory/Voluntary
- Privacy by design/default
- Data privacy impact assessments

### Lawful basis for processing

This is necessary for the following:
- For the performance of a contract
- Legal obligation
- To protect vital interests
- Tasks carried out in public interest
- Legitimate interests
- Consent actively given
	- Any freely given, specific, informed and unambiguous indication of the data subject's wishes by which he or she, by a statement or by a clear affirmative action, signifies agreement to the processing of personal data relating to him or her
- There are exceptions for special categories, such as medicine or public health.

### Individual Rights

- Information
- Subject access
- Rectification
- Erasure (Right to be forgotten)
- Portability
- Objecting
- Compensation
- Profiling
- Restriction

### GDPR and Information Security

- Manage risk
- Process data securely
- Protect personal data against cyber attack
- Minimise impact of incidents
- Must notify breaches
- Big fines for non-compliance

#### Managing Risk
- Map the law to your processing
- Identify key data processing
- Identify high-risk processing
- Identify gaps
- Mitigate the risks
- The 6 Ws:
	- *Why is personal data processed?*
	- *Whose personal data is processed?*
	- *What personal data is processed?*
	- *When is personal data processed?*
	- *Where is personal data processed?*
	- *How is personal data processed?*

GDPR defines appropriate procedures in A.1 and A.2.

##### A.1 Governance

You have appropriate data protection and information security policies and processes in place. If required, you ensure that you maintain records of processing activities, and have appointed a Data Protection Officer.

##### A.2 Risk management

You take appropriate steps to identify, assess and understand security risks to personal data and the systems that process this data. You also make effective risk-based decisions based upon the following:

- The state of the art \[of technology\]
- Cost of implementation
- The nature/scope/context/purpose of processing
- The severity and likelihood of risks being realised.

Where processing is likely to result in a high risk to the rights/freedoms of individuals, you must also undertake a Data Protection Impact Assessment to determine the impact of the intended processing on the protection of personal data.

#### Processing Personal Data

##### A.3 Asset management

You understand and catalogue the personal data you process and can describe the purpose for processing it. You also understand the risks posed to individuals of any unauthorized or unlawful processing, accidental data loss, destruction or damage to that data.

The personal data you process should be adequate, relevant and limited to what is necessary for the purpose of the processing, and it should not be kept for longer than is necessary.

##### A.4 Data processors and the supply chain

You understand and manage security risks to your processing operations that may arise as a result of dependencies on??third parties??such as data processors. This includes ensuring that they employ appropriate security measures.
   
You are required to choose data processors that provide sufficient guarantees about their technical and organisational measures. The GDPR includes provisions where processors are used, including specific stipulations that must feature in your contract.

#### Process data securely

Article 5(1)(f) states that personal data shall be:

*Processed in a manner that ensures appropriate security of the personal data, including protection against unauthorised or unlawful processing and against accidental loss, destruction or damage, using appropriate technical or organisational measures*

In summary, take appropriate action, such as doing a risk assessment. The security measures must be designed into your systems at the outset, a process referred to as *Privacy by Design.*

Article 25 mandates that, at the time of the *determination* of the means of the *processing* (i.e. the design phase of any processing operation) and at the time of the processing itself, appropriate measures must be put in place.

#### Protect personal data against cyber attack

You have proportionate security measures in place to protect against cyber attack which cover the personal data you process, and the systems that process such data.

You should appropriately authenticate and authorise users (or automated functions) that can access personal data. You should??strongly authenticate users who have??privileged access and consider two-factor or hardware authentication measures.

You should prevent users from downloading, transferring, altering or deleting personal data where there is no legitimate organisational reason to do so. You should appropriately constrain legitimate access to ensure there is an appropriate audit trail.

You should have a??robust password policy??which avoids users having weak passwords, such as those trivially guessable. You should change all default passwords and remove or suspend unused accounts.

- Actively managing software vulnerabilities, including using in-support software and the application of software update policies (patching) and taking other mitigating steps, where patches can???t be applied.

- Managing??end user devices??(laptops and smartphones etc) so that you can apply??organisational??controls over software or applications that interact with or access personal data.

- Encrypting personal data at rest on devices (laptops, smartphones, and removable media) that are not subject to strong physical controls.

- Encrypting personal data when transmitted electronically.

- Ensuring that web services are protected from common security vulnerabilities such as SQL injection and others described in widely-used publications such as the??OWASP Top 10.

- Ensuring your processing environment remains secure throughout its lifecycle.

- You also undertake regular testing to evaluate the effectiveness of your security measures, including virus and malware scanning, vulnerability scanning and??penetration testing??as appropriate. You record the results of any testing and remediating action plans.

- Whatever security measures are put in place, whether these are your own or whether you use a third party service such as a cloud provider, you remain responsible both for the processing itself, and also in respect of any devices you operate.

##### B.1 Service Protection Policies and Processes

You should define, implement, communicate and enforce appropriate policies and processes that direct your overall approach to securing systems involved in the processing of personal data. You should also consider assessing your systems and implementing specific technical controls as laid out in appropriate frameworks, such as ISO 27001.

##### B.2 Identity & Access Control

You understand, document and manage access to personal data and systems that process this data. Access rights granted to specific users must be understood, limited to those users who reasonably need such access to perform their function and removed when no longer needed. You should undertake activities to check or validate that the technical system permissions are consistent with your documented user access rights.

##### B.3 Data Security

Implement technical controls (such as appropriate encryption) to prevent unauthorised or unlawful processing of personal data, whether through unauthorised access to user devices or storage media, backups, interception of data in transit or at rest or accessing data that might remain in memory when technology is sent for repair or disposal.

##### B.4 System Security

Implement appropriate technical and organisational measures to protect systems, technologies and digital services that process personal data from cyber attack.

Whilst the GDPR requires a risk-based approach, typical expected examples of security measures you could take include:

- Tracking and recording of all assets that process personal data, including end user devices and removable media.
- Minimising the opportunity for attack by configuring technology appropriately, minimising available services and controlling connectivity.

###### B.5 Staff awareness & training

You give staff appropriate support to help them manage personal data securely, including the technology they use. This includes relevant training and awareness as well as provision of the tools they need to effectively undertake their duties in ways that support the security of personal data.

Staff should be provided with support to ensure that they do not inadvertently process personal data (e.g. by sending it to the incorrect recipient).

#### Minimise impact of incidents

- Measures to detect security events
- Resilience of processing systems/services
- Ability to restore availability to personal data in event of an incident

##### C) Detect security events

You can detect security events that affect the systems that process personal data and you monitor authorised user access to that data

###### C.1 Security monitoring
   
You appropriately monitor the status of systems processing personal data and monitor user access to that data, including anomalous user activity.

You record user access to personal data. Where unexpected events or indications of a personal data breach are detected, you have processes in place to act upon those events as necessary in an appropriate timeframe.

##### D.1 Response and recovery planning

You have well-defined and tested incident management processes in place in case of personal data breaches. You have mitigation processes are in place that are designed to contain or limit the range of personal data that could be compromised following a personal data breach.

Where the loss of availability of personal data could cause harm, you have measures in place to ensure appropriate recovery. This should include maintaining (and securing) appropriate??backups.

##### D.2 Improvements

When a personal data breach occurs, you take steps to:
- Understand the root cause
- Report the breach to the Information Comissioner and, where appropriate, affected individuals
- Where appropriate (or required), report other relevant bodies (for example, other regulators, the NCSC and/or law enforcement) and 
- Take appropriate remediating action.

#### Must notify breaches

- Personal data breach
	- Notify Information Commissioner???s office within 72 hours of discovery

- You may also wish to??report significant cyber incidents??to the National Cyber Security Centre.
	- If the incident is likely to have a national impact then we will seek to provide support, subject to resource constraints.
		- National impact includes harm to national security, the economy, public confidence, or public health and safety.
	- NCSC also welcome notification of incidents ???for information??? which you feel may be of interest, for example incidents which may contribute to our understanding of adversary activity, inform the guidance we provide, or help other organisations.

- Incidents below national threshold should be reported to??Action Fraud????? the UK???s national fraud and cyber crime reporting centre or, if you're in Scotland, then reports should be made to??Police Scotland.

#### Fines for non-compliance

- Sanctions for non-compliance
- Supervisory Authorities
	- Investigative powers
	- Corrective powers
- Penalties
	- 2% global turnover or ???10m (whichever is greater)
	- 4% global turnover or ???20m for serious incidents
	- Turnover, not Profit
		- TalkTalk profit 2017: $165 million
		- Turnover 2017: ??1.783 billion
- Compensation

