#isys20311-infosec/lecture-8
# Procedural & Physical Controls

## Procedural Controls

Information assurance refers to more than just a range of technical security countermeasures; *people*, as the largest source of vulnerabilities, must be educated, motivated and appropriately regulated.

Procedural controls therefore aim to inform and guide user behaviour within the security context the ISMS defines; but while policies and guidance will exist, their efficacy is limited if security culture within an organisation is poor.

### Security Culture

Even the most expensive controls are worthless with employees that are not security conscious. They need to know about the relevant dangers, why they matter to them, and how the assets they use are protected - alongside being able to act according to defined procedures and knowing what potential incidents might look like, in order to make immediate reports.

Such changes to corporate culture cannot be done just in isolated departments; it must be implemented from the top and throughout every level of the organisation.

### Security Awareness

Security awareness programs should aim to develop employees in the education of key threats and organisational risks. This is usually done as part of induction into a new job, where the employee is taught what risks are specific to the organisation they work in and the potential impact of breaches. Knowledge of laws and regulations may also be important.

Records should be kept of which employees have gone through training, and refresher sessions should be deployed as needed; it should not be a one-time event.

### Contracts

Alongside usual terms of employment, contracts typically have some detail regarding acceptable behaviour, which may include:

- Acceptable asset use
- Disciplinary processes
- Confidentiality of information
- Intellectual property rights

### Code of Conduct

Codes of Conducts may place obligations on employees regarding information assurance. They may also include the ethics and standards of the organisation, outlining behaviour in regard to colleagues and external parties, alongside social media guidance and other items that seek to reduce the risk of social engineering vulnerabilities, such as the receipt of gifts or inducements.

### Acceptable Use Policies

These outline behaviour in regard to the organisations information and communications systems, and are designed to protect the organisation in event of employee error by exercising due diligence in telling staff what cannot be done with company assets.

They may also outline disciplinary steps if rules are broken; the goal is to deploy a positive security culture, so this is often a difficult policy to introduce.

### Password Policies

Of note is what kind of authentication mechanism is demanded to maintain security; if passwords are used, documents may dictate the strength of a password and how often it needs to be changed. They may also consider number of failed attempts, and whether passwords should be combiend with further authentication methods such as keycards or biometrics. Access points should also be defined and authentication measures asssured for each AP.

### Segregation of Duties

One individual should not perform duties for more than one role, where conflicts of interest are present. The scope of attack for any single individual needs to be controlled - one person should not have total admin rights for the whole organisation, for example.

Segregation of duties is sometimes required by legal bodies in the context of some industries, but the practice generally also helps limit an organisation's dependence on on individual.

#### Information Classification

Segregation of duties works on a 'need-to-know' basis; staff only have access to what they need to perform their business processes, both in terms of assets and data.

Assets themselves will have a defined owner who has full control, deciding what level of control others have; data should be labelled  with the organisation's information classification policy.

##### Data Labelling

An organisationally defined agreed impact system that tags data based on its sensitivity is essential (e.g. confidential, internal only, public).

Data labelling is based on the impact if CIA is breached; classification defines who can view data alongside how it should be stored and destroyed.

###### Storage/Deletion Policies

Policies on data storage and deletion need to abide by legal requirements, such as the GDPR & Data Protection Acts. As a general rule, data should usually be encrypted both while at rest and in transit; steps must be taken to securely destroy data when no longer required or in order to comply with regulation, and data mapping should be carried out in order to understand the information flow and potential points of vulnerability.

### Other Common Policies

#### Bring Your Own Device (BYOD)

Organisations must decide if this is allowed and if so, how it will be managed - for example, are employees allowed to work from home?

#### Removable Media

Are employees allowed to take work home using an external device, or should their use be prohibited?

#### Away From Desk/Clear Desk

Automatic time-outs on inactive machines when logged out are sometimes implemented; the organisation must decide on how long these should be. Some organisatons also require desks to be kept free of clutter, in order to prevent sensitive information being kept out in the open.

## Physical Controls

These refer to reliance on the presence of physical objects to deter criminal activity. The goals of physical security are as follows:

- **Deny** - prevent malicious action
- **Deter** - make malicious action an unatttractive proposition
- **Detect** - catch malicious action
- **Delay** - slow down malicious action
- **Defend** - respond to malicious action

Examples include, but are not limited to:

- **Perimeter defences** such as walls, doors, CCTV, keycards and lighting.
- **Personnel** such as security guards.
- **Architectural design** such as air gaps.

### A Tiered Approach

This method ensures that there is no *one* control for *one* risk, as it is dangerous to create a security plan that makes a singular recommendation without review - a combination of controls must be put in place that simultaneously act both as effective technical countermeasures and to guide behaviour such that they are used acceptably.

For example, the use of card readers and security guards alongside a policy on taking deliveries.

#### Examples of Security Controls

An example table is shown below:

| Preventative | Detective | Corrective | Compensatory |
| ------------ | --------- | ---------- | ------------ |
| Security/Awareness Training | System Monitoring | OS Upgrade | Backup Generator |
| Firewall | IDS | Backup Data Restoral | Hot Site |
| Anti-virus | Anti-virus | Anti-virus | Server Isolation |
| Security Guard | Motion Detector | Vulnerability Mitigation | |
| Policies | Security Guard |  |  |