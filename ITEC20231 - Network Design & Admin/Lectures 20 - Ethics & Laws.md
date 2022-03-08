# Ethics & Laws
## Security in General

Three different aspects can be considered regarding the security of the network:
1) Security against legal claims/cases
2) Security against physical disaster/hardware failure
3) Security against attackers
4) Security against software failure
	- E.g. program with memory leak gradually kills system
		- Monitoring should help with this

## Ethics, Laws and Standards
For a simplistic view of the differences:
- **Ethics** - non-conformance results in bad publicity
- **Laws** - non-conformance can lead to arrest
- **Standards** - if not certified, credibility can be lost

We should care about these as Systems/Network admin because the buck could stop with us and we could be held accountable and/or prosecuted.

### Ethics
A good company will try to behave ethically to its employees, customers and suppliers. This will involve production and publication of a [Code of Conduct](https://www.usenix.org/lisa/system-administrators-code-ethics) - which goes beyond the law. Basic concepts include:
- Accountability
- Responsibility
- Liability

Examples of ethics within a company include:
- E-mail checking
- Monitoring internet use
- Blocking websites

A few questions, however:
- When is it right to read other people's e-mail?
- Why would internet use need monitoring?
- What websites should be blocked?
- What about offensive images on desktops?

### Laws/Acts that can affect IT Companies

Laws can be broken in two ways; by committing an offence, or by omission. Sys/Network admins and managers need to be aware of the following laws at minimum:
- *Copyright Designs and Patents Act 1988*
- *Electronic Commerce (EC Directive) Regulations 2002*
- *Data Protection Act 1998*
	- Including the changes made in 2018 via the GDPR
- *[Disability Discrimination Act 1995](https://www.rnib.org.uk/xpedio/groups/public/documents/publicwebsite/public_legalcase.hcsp)*
- *[Sexual Offences Act 2003](http://www.computing.co.uk/itweek/news/2085638/rules-cut-porn-risks)*
- *Investigatory Powers Act 2016*
- *Telecommunications* - (Lawful Business Practice) (Interception of Communications) Regulations 2000 (LBP Regulations)
- *Article 8 of the Human Rights Act 1998*
- *Privacy and Electronic Communications* (EC Directive) Regulations 2003
- *[Part 11 of the Anti-Terrorism, Crime and Security Act 2001](http://www.opsi.gov.uk/acts/acts2001/ukpga_20010024_en_11)*
- *Counter-Terrorism and Security Act 2015* (Communications Identity)#

#### Copyright Act
Software is considered as a piece of literary work. FAST applies Copyright Law against companies, and companies blame IT/System administrators. How can we keep a check on copyright within the company?
- Keep good control on licenses; where possible, use site licences or licence servers.
- Ensure no pirated software is added by users.
- Ensure copying of documentation/printing of information from the internet follows the CLA(?).

#### E-Commerce Requirements
Sources: http://www.out-law.com/page-431 and the OFT publication *"A guide for businesses on distance selling"*

Both those responsible for a website, as well as service providers - whether involved in e-commerce or not - should provide the following minimum information, which should be easily, directly and permanently accessible:
- The *name* of the service provider must be given somewhere easily accessible on the site.
- The *email address* of the service provider must be given. It is not sufficient to include a 'contact us' form without also providing an email address.
- The *geographic address* of the service provider must be given.
- If a company, the company's *registration number* should also be given.
	- The *place of registration* should also be stated.
		- This is required by the *Companies Act* as from 31st December 2006.
- If the business is a member of a trade or professional association then membership details - including any registration number - should be provided.
- If the business has a *VAT number*, it should be stated - even if the website is not being used for e-commerce transactions.
- Prices on the websites should be clear and unambiguous.

The *Distance Selling Regulations* contain other information requirements for online businesses that sell to consumers (business-to-customer, as opposed to business-to-business sales).

#### Data Protection Act 1998

Organisations that process personal information must register with the *Information Commisioner (IC).* Such bodies must have adequate technical and organisation security protection in place.

Data may only be used for the specific purpose for which it was collected; it may not be transmitted outside the EEA without consent (or adequate protection), and must be kept "no longer than necessary".

##### Understanding the DPA

![[Pasted image 20220308015315.png]]

##### How does it affect sysadmins?
If you are the *Data Controller,* the IC may:
- Assess your data processing setup for good practice, with you permission (Section 51(7))
- Serve you with a notice for information (Section 43)
- Get a search warrant from a judge to inspect your setup (Section 9)

*"Any person who intentionally obstructs the Commissioner, or fails without reasonable excuse to give any assistance reasonably requested, is guilty of an offence"*

The 1998 act is being superseded by the GDPR in May 2018.

#### [General Data Protection Regulations (2018)](https://www.itgovernance.co.uk/data-protection-dpa-and-eu-data-protection-regulation)
- Need to ensure accountability/governance compliance
	- Detailed governance structures with roles/responsibilities
	- Detailed record of all data processing operations
	- Documenting policies and procedures
	- Data protection impact assessments
	- Appropriate measures to secure data
	- Staff training and awareness
	- Data protection officer required (as with DPA 1998).

GDPR is based on similar principles to the DPA that it supersedes:
- Data is processed lawfully/fairly/transparently
- Collected and used for a specific purpose
- Only relavant information for purposes is captured
- Data is accurate and kept up-to-date
- Data is only stored as long as necessary
- Processed in a manner that ensures appropriate security

The GDPR gives individuals enhanced rights, that include the right to:
- Be informed
- Access their data
- Rectify their data
- Erasure of data
- Restrict data processing
- Data portability
- Object to data collection
- Rights in relation to automated decision making/profiling of data

#### Privacy and Electronic Communications (EC Directive) Regulations 2003

If there is a significant security risk associated with using your service, you *must inform the user* of:
1) The nature of that risk (e.g. tracking via cookies);
2) Any appropriate measures that the subscriber may take to safeguard against that risk (e.g. private browsing);
3) The likely costs to the subscriber involved in the taking of such measures (e.g. more software)

This is now law, but do *all* online companies do this?

The EC Directive also:
- Prohibits unsolicited commerical marketing by e-mail without 'opt-in' consent:
	- But the regulations do not help with most spam.
- Requires you to inform users about any cookies or what web bugs do, and the information they collect.
	- One interpretation is that you must allow users to refuse the cookies.
- However, the IC takes a [more pragmatic view.](http://www.aboutcookies.org/Default.aspx?page=3) 
- Information used for the provision of a service must be erased/anonymised after completion of the transmission.

#### Sexual Offences Act 2003
If an employee accesses illegal material or saves it on shares, what happens? There is the potential for bad corporate publicity and cost, since police may take machines away for a considerable time, and probably take backup tapes too.

Often, sysadmins/managers are also worried about reporting such material, in case they are also considered responsible. There is a memorandum of understanding between CPS and the police clarified by law, that allows sysadmins/managers to preserve such files, but only in order to [present it to police](http://www.iwf.org.uk/police/page.22.213.htm) by reporting it to the Internet Watch Foundation.

Good practices will involve web controls, traffic and storage-use monitoring.

#### Disability Discrimination Act 1995
It is unlawful for "a provider of services" to discriminate against a disabled person in failing to comply with provisions of the DDA. 

An example case would include *Sydney Olympics* (McGuire vs. SOCOG 2000)

