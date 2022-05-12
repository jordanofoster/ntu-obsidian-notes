# Assets

## Assets
Assets are anything that has value and contributes to the operation of a business. Asset identification tends to be the first stage in risk assessment, and the eventual goal of it is to produce an asset register, which lists all key assets and who is responsible.

### Asset Identification
![[AssetIdentRing.png]]
There are several different types of asset:

- **Information**, stored electronically, on paper, etc.
- **Software** such as Operating Systems, Applications, Dev tools, etc.
- **Physical** assets or Hardware; this refers to any asset that can manipulate information.
	- Computers, servers, wiring, fibre...
- **Supporting services**, such as heating, cooling, power, lighting...
- **People** who carry the skills and/or knowledge to support/implement business processes.
- **Intangible assets** such as brand and reputation.

### Information
Information does not only include digital assets within databasses, but also things kept of removable media (if allowed) and traditional paper documents. Information can also include knowledge held by staff members (especially business critical information).

Information is either taken from another source, such as customer details or buying datasets, or created from scratch (e.g. from companies that focus on research and development).

#### Information Life Cycle.
The diagram below shows the information life cycle in its simplest form:

![[InformationLifeCycle.png]]

##### Acquisition

Information may be acquired from a number of sources:
-	Through web portals and dedicated interfaces;
-	or forms completed during business processes.

Processing of information is typically required to make information useful, such as attaching relevant metadata (e.g. permission level), and business data (which project, who owns it). Policy controls are used to encrypt data where need such as Personally Identifiable Info (PII), classification etc.

##### Use

After the information has been prepared and stored, it is utilised as part of business operations; read and modified by a variety of users (hence why defining metadata is important during acquisition). The Use phase is arguably the most challenging phase when attempting to maintan the CIA triad, as data must be available but only to the right people (a challenge in and of itself). Internal consistency of data tends to be a problem also, when working across multiple data stores where replication/modification is required.

##### Archival

A major question is what happens when information is not used for a while in an organisation - changes or unauthorised access/modification can go undetected for long periods of time without appropriate controls.

Archival processes can form the basis for back-ups, but backups are distinctly **not** archives. Controls for archived datasets include encryption at an absolute minimum.

##### Disposal

Attention should be paid to when information is deleted; too soon, and recovery is impossible after a breach - too long, and costs are impacted or data compliance and regulation legislature can be accidentally breached.

There must be certainty that data is properly destroyed. Physical devices can be wiped, degaussed, or shredded depending on medium, but distributed data is harder to remove - and third parties are another question entirely.

![[DisposalDiag.png]]

### Infrastructure

What infrastructure is used in each stage determines identification of threat vectors and impacts risk analysis. All infrastructure used are also key assets, blurring the line between different types. Security of Servers, Networks, Databases and Hosts are also a key consideration.

### Software/Services

Both provide access to data or the means to process it. The hope is that data is accurate, but the algorithms that process it must also be considered. They are distributed throughout the network on hosts machines, servers and customer-facing websites. Denial of service in this instance can prevent access to information.

### Physical Assets

Refers to the hosts and houses the software/business has, and provides communication channels between other assets. There is some overlap when talking about potential attacks but physical damage tends to be the main threat - although elements of network attacks are also considerable.

### Systems and Services
The focus here is on support systems as part of wider contexts; this includes IT support infrastructure, environmental controls, financial/legal support where appropriate. Disasters such as power going down should also be considered - not just attacks.

### Human assets

Staff members or other key stakeholders that contribute to the running of an organisation - often having knowledge/skills/experience that is irreplacable. Humans tend to be the single biggest source of vulnerabilities for threat exploitations, and this is not just limited to attacks - high staff turnover rates can also be dangerous for keeping information secure.

### Intangible assets

These refer to a broader organisational idea, such as brand or reputation. These differ from company to company and can be more or less important depending on purpose. Attacks cannot be carried out *against* these as they don't exist, but attacks on other assets can be carried out with the aim of compromising these.

Defining them and the potential damage that attacks can do is an important part of making a comprehensive ISMS.

### Asset classes/Process Analysis

This is a list of all identified resources per asset class:
- Information
- Software
- Physical/hardware
- Services
- People
- Intangibles

Can also be created through an initial key process and breakdown of critical resources to identify key assets and the RTO.

### Estimating RTO

How long can organisations continue without an asset being available? Generally, these are categorised, for example:

- Non-essential: 30 days
- Normal: 7 days
- Important: 72 hours
- Urgent: 24 hours
- Critical: minutes/hours

Estimates help calculate both risk and impact, and determine what controls should be implemented - such as "critical assets should have strong back-ups and redundancies present." An example diagram is shown below:

![[EstimatingRTODiag.png]]

### Assigning Value to Assets

Assets, when identified, should be classified according to value to its relevant process. Questions that are asked include:

- Will it lead to any of the following:
	- Loss of reputation?
	- Competitive advantage?
	- Increase in operational expenses?
	- Violations of contract/legal requirements?
	- Delayed income?
	- Revenue?
	- Productivity?

The importance of these depends on the business affected.

#### Asset Registers

This is a table that lists all assets, their importance/evaluation and who is accountable. The individual accountable should be involved in resulting risk analysis. An example is shown below:

| Process/Asset Class | Asset | Likelihood of damage/loss | Impact of damage/loss | Value | Owner | Comments |
| ------------------- | ----- | ------------------------- | --------------------- | ----- | ----- | -------- |
| Sales | Customer credit card database | Low | Very High (RTO: Urgent) | Reputation: Very high Regulatory fines: High | Sales Manager | Data at rest: Should this be owned by the IT department? |
