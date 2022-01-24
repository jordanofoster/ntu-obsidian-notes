# Business Continuity

*'A holistic management process that identifies potential impacts that threaten an organisation and provides a framework for building resilience with the capability for an effective response that safeguards the interests of its key stakeholders, reputation, brand and value-creating activities.'* (Business Continuity Institute, 2001).

## Why does it matter?

Without business continuity, the following can happen:
- Loss of work to competitors
- Failures within the supply chain
- Loss of reputation
- Human Resources issues
- Health and Safety liabilities
- Higher insurance premiums

40% of businesses affected by the Manchester bombing went out of business permanently, as they did not have business continuity.

## How is it done?

In short; make policies and ensure that they are followed. An ISO standard exists for organizations to reach business continuity with, and be certified for.

### ISO/IEC 27031

This refers to *Security Techniques - Guidelines for information and communication technology readiness for business continuity.* In other words, this is the familiar Plan-Do-Check-Act cycle, as shown below:

![[Pasted image 20220124144308.png]]

#### Additional rules for emergency services, local authorities and utility companies

The *Civil Contingencies Act 2004* exists to enforce this. Part 1 of the Act places a legal obligation upon emergency services and local authorities (defined as *"Category 1 responders"* under the act) to plan, exercise for and assess the risk of emergencies, as well as undertaking Business Continuity Management.

Category 1 responders are also responsible for warning and informing the public in relation to emergencies, and local authorities are required to provide business continuity advice to local businesses.

It also places legal obligations for increased cooperation and information sharing between different emergency services and also to non-emergency services that may have a role in emergency situations (such as electric companies). Such non-emergency services are defined as *Category 2 responders* under the Act.

Each responder has an emergency planning officer, sometimes called a civil protection, civil contingencies or resilience officer (or also alternatively, simply 'risk manager') who is usually responsible for ensuring their organisation is in compliance with the Act and sharing information with other responders. The usual way of checking compliance is by regularly testing plans by reviews or exercises.

## Differences between BC and Backups

### Tiers of preparedness

SHARE released a 7-tier disaster recovery released in 1992, updated in 2012 by IBM as an 8-tier model. It is listed below:

- Tier 0
	- Nothing off-site. Recovery time is unpredictable - recovery itself is perhaps not possible.
- Tier 1
	- IBM calls this PTAM (*Pickup Truck Access Method*) - this is on a hotsite, however (using backup hardware).
-  Tier 2
	- Hot site - requires hours/days to load even the most recent backup tapes.
- Tier 3
	- Transaction data at off-site kept relatively current, using ongoing high-speed data link (electronic vaulting) and "an automated tape library at the remote site."
- Tier 4
	- "Point-in-time copies", to ensure that less reprocessing of transactions are needed.
- Tier 5
	- "Transaction integrity", where the hotsite is kept as up-to-date as possible (to the moment).
- Tier 6
	- "Zero or Near-zero data loss"
- Tier 7
	- "Highly automated" recovery - few if any manual steps are required following a main site failure; rollover to the hotsite is automatic.

## Problems are not just cyber attacks

These include:
- Epidemics
- Earthquakes
- Fires
- Floods
- Sabotages (insider/external threat)
- Hurricanes/other major storms
- Power outages
- Water outages (supply interruption, contamination)
- Telecoms outages
- IT outages
- Terrorism/Piracy
- War/civil disorder
- Theft (insider or external threat, vital information or material)
- Random failure of mission-critical systems
- Single point dependencies
- Supplier failures

### In disaster scenarios, problems interact

For example:

- Emergency teams cannot locate people if the mobile network is down.
- Disaster zones can still be hot/flooded/unstable/infectious/irradiated long after a disaster.
- Nuclear plant shutdown procedures may fail if the electricity fails
- Normally rational human beings may start acting out of desperation

##### Planning for Interactions

During the 2002-2003 SARS outbreak, some organizations compartmentalized and rotated teams to match the incubation period of the disease. In-person contact was also banned during both business and non-business hours; these steps increased resiliency against the threat.

##### Other effects of disasters that go beyond backups

It may take a long time for a business to occupy its original premises (if ever!). Additionally, equipment in buildings may be damaged by rescue efforts as well as by the disaster.

#### IT-related disasters and continuity

- IT equipment destroyed
- Data destroyed by malware
- Payment/personal data is stolen
- Data manipulated (e.g. sending payments to different addresses)
- Piracy: (stolen data is used in a different jurisdiction)

Any of the above can happen to a key supplier; for example, British Airways had an issue with a 3rd-party flight booking website.

## What do BCPs need to consider?

For IT, minimum application/data requirements and the time in which they must be available is to be considered. Outside of IT, hard copies (such as contracts) must be preserved. Manufacturers (processing plants for example) must consider skilled staff and embedded technology.

BCPs need policies for at least the following:
- Crisis management command structure
- Telecommunication architecture between primary and secondary work sites
- Data replication methodology between primary and secondary work sites
- Backup work sites - applications, data and workspaces required at the secondary work site.

### Plan Checklist

- Emergency response
- Crisis management
- 




