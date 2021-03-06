#isys20311-infosec/lecture-15
# Legal Proceedings

## Requirements for electronic evidence

- Evidence must be obtained using legal methods.
- Evidence must follow certain rules:
	- Is it relevant and neccessary?
	- As stated before, has it been acquired legally?
	- Does it comply with procedural requirements, and thus is procedurally admissible?
- Electronic evidence should be evaluated:
	- It can be challenged by an opposing party on the following grounds:
		- For example, the authenticity of an email conversation
		- Or just generally, the ingerity and accuracy of the evidence.

## Admissible Evidence

Evidence must follow a chain of custody; for example, records of everyone who has touched or could have otherwise modified data on that machine after the incident, until the forensic image has been taken.

The easiest way is to stop anyone from touching it.

Regarding forensic images themselves; they are typically accepted in court if hash values have been verified - but some jurisdictions and police forces may want the original computer untouched in case the court asks for another verification.

If evidence is on social media or private email, sometimes ISPs can be forced to release information with a court order.

## Criminal or Civil

If it is possible to identify the perpetrator of an information security breach, the breach itself may fall under criminal or civil law, so the victim may have a choice on which charges to press. If criminal charges are pressed, the police becomes involved, and jail sentences are able to be given; however the courts will only deal criminal charges if the accused is guilty beyond reasonable doubt.

If civil charges are pressed, solicitors are involved - fines for damages are available, and a balance of probabilities is required.

### Criminal Law

#### Theft

The key damage in many breaches is the unauthorised obtaining of information. The main question is whether this is theft; the legal definition is as follows:

*\[theft is] appropriating property belonging to another dishonestly with intent to permanently deprive.* 

This shows that information theft is *explicitly* excluded from the Theft Act 1968, and court cases have upheld this interpretation of the law (see *Oxford v. Moss, 1979*).

#### Fraud Act 2006

This updated various offences originally prosecuted under the Theft Acts. Under this act, it is an offence to do the following with intent of making gain for yourself or loss for another:
- Make a false representation
- Fail to disclose information that you are legally required to disclose
- Abuse a position of safeguarding financial interests

The act also makes it an offence to possess or make articles for use in frauds.

#### Computer Misuse Act 1990

This Act was originally design to deter hackers. Unauthorised access to a computer is defined as a summary offence, with a max sentence of 6 months. The unauthorised *modification* of a computer can be an offence of either kind, but contains a larger max sentence of 2 years.

An extension of this, the Serious Crime Act of 2015, gives a maximum sentence of 14 years for causing damage to an economy or environment. [See this telegraph article.](https://telegraph.co.uk/news/2017/04/09/hacker-sets-every-emergency-siren-dallas/?)

Denial of service is also covered by case law under this Act (See *DPP v. Lennon, 2006*). A summary of the case is as follows:

- The defendant (Lennon) was dismissed from his employment. He subsequently sent several hundred thousand emails to his former employer's computer system which purportedly came from the company's HR manager.
- Charges were brought under Section 3 of the Computer Misuse Act 1990 for making an unauthorised modification to the contents of a computer.
- The judge, at first instance, held that the emails were authorised as the employer's computer system was set up to receive email. It was also held that Section 3 was designed to prevent the sending of material such as computer viruses.
- On appeal, the High Court concurred that a person who sets up a computer to receive emails is giving consent to emails being sent to that computer.
	- This consent does not extend to emails sent not for communication purposes, but to disrupt the system.

Making, supplying or obtaining articles for use in computer misuse offences is also a crime under Section 37 of the *Police and Justice Act* - A controversial decision.

Making information available with intent (such as other people's passwords) is not yet a criminal offence, but the concept is under discussion since the *News International* phone hacking scandal of 2011.

#### GDPR

The EU-wide General Data Protection Regulation took effect on the 25th May 2018. It updates the Data Protection Act of 1998 - with the biggest change being a huge increase in fines; to show an example, under UK law TalkTalk was fined ??400,000 - under GDPR, this fine would be predicted as large as ??52 *million.*

##### Other changes under GPDR

Individuals must give 'clear and affirmative consent' to the processing of their data. A checkbox is adequate; anything less (read: silence) is not. IP addressses and mobile device IDs are unquestionably defined as personal data; their status was previously questionable under the Data Protection Directive.

Genetic and biometric data are classified as 'sensitive personal data.' There is a strong incentive to pseudonymise data sets - such data is still classed as personal data, but is exempted from various GPDR requirements. Encryption of data is also encouraged.

The 'right to be forgotten' established by the European Court of Justice (See *Google Spain v. AEPD,* 2014) has been extended towards a 'right to erasure' - it is no longer sufficient to remove a person's data from search results under a request; data controllers must now erase that data entirely. However if the data is encrypted, it may be sufficient to destroy the keys rather than undergo the prolonged process of ensuring that the data is fully erased.

##### Complying with GDPR

Text-based checklists are available, provided by various organisations including the Information Commissioner's Office, for organisations to use when preparing to comply to GDPR. To provide an examplem under Article 39:

*"Data Protection Officers are under a specific obligation to implement appropriate training. Although not an express obligation for organisations where DPOs are not required, we consider it to be almost impossible to demonstrate that an organisation is able to achieve compliance without policies setting out how to comply coupled with training to bring those policies to life."*

Regarding the checklists themselves:

*"Organisations should implement a training programme covering data protection generally and the areas that are specifically relevant to their organisations, and implement a policy for determining when training should take place and when refresher training should be carried out and a process for when training has been completed"*

##### Unresolved Issues

- DPOs are required to offer training, but do staff have to accept it?
- Which staff need to be trained?
- If multiple jurisdictions are involved, which supervisory authority or authorities should take action?
- Who (or what) decides whether training is adequate or suitable?
- If an organisation does not require a DPO, does it truly have no requirement to train its staff in data processing issues? Might there be a requirement under contract or tort law?
- What do words such as "regular" and "large-scale" mean?

Decisions made by the European Court of Justice are expected to bring light to some of these issues caused by the legislative text itself.

##### Who is the threat?

Under GPDR, are organisations a threat to cloud service providers and the companies they support? See below:

![[Pasted image 20220202001913.png]]

![[Pasted image 20220202001927.png]]

##### A particular issue for AI/ML systems: responding to requests for personal information

Articles 13-15 of GDPR require that the data subject be given a variety of information about their rights regarding the storage and processing of their personal data, including "the purposes of the processing for which the personal data are intended." 

If subjects' personal data is being used for "automatic decision making including profiling" then they are also entitled to "meaningful information about the logic involved", as well as "the significance and the evisaged consequences of such processing for the data subject."

Article 22 of GPDR spells out the purpose of these requirements: that "the data subject shall have the right not to be subject to a decision based solely on automated processing, including profiling, which produces legal effects concerning him or her or similarly significantly affects him or her."

Is this impossible for machine learning systems to deliver? The GDPR does explicitly state that data subjects have a right to "obtain an explanation of the decision reached after such an assessment", but in Recital 71 (which is non-binding), rather than in the legally binding Articles.

It *is* possible to provide "meaningful information about the logic" and to explain the "significance of decision making" without giving a full explanation of an individual decision - this is done by providing a document giving a technical description of the ML model. One unreferenced article suggests describing where the data comes from, the method used, and how many features are selected for.

Another document is suggested to give an understanding of the decision(s) that the model is used to make and the consequences of a false positive or an omission. This will help to explain not only the logic of the decision, but also its significance.

#### Intellectual Property Law

IP law only applies if the thief *actually uses* the stolen information; at least in this instance there is someone to prosecute, though.

Under patent law, a patent is theoretically breached after the theft of information, but this rarely applies, as the purpose of patents is to persuade inventors to publish their designs in return for a limited monopoly on its use - so as a result, theft is unneccessary (it's already public knowledge!)

Violation of copyright law is relatively easy to prove, via similarity - but it protects form and not function; if the design for a market-leading chocolate bar was stolen and reproduced, the law would only protect the wrapper and the shape of the bar itself, and not the creation process.

Copyright law includes the database right, defined under Section 16 of the CDPA. It covers any organised collection of independent works (see *British Horseracing Board v. William Hill*, 2004). Offences are defined as *unauthorised extraction or re-utilisation of all or a substantial part of the contents of the database,* or the *repeated and systematic extraction or re-utilisation of insubstantial parts of the contents of the database.*

Trademark law applies if someone uses a similar trademark to you, but only *within your legal jurisdiction.*

### Civil Law

#### Breach of Confidence

This was originally designed to protect trade secrets, so that anyone who learned of one under a confidentiality agreement could not reveal it. Key factors of the law include the following:

- The information has "the neccessary degree of confidence about it"
- The information was provided in circumstances importing an obligation of confidence
- There was an unauthorised use or disclosure of that information and, at least, the risk of damage

The concept has been progressively broadened by case law decisions:

- *Saltman Engineering Co. Ltd. v. Campbell Engineering Co. Ltd.* (1948) has the court rule that "No contractual relationship is required". 
- *Douglas v. Hello!* (2002), a case initially concerning the confidentiality of electronic information in the context of photographs, had the courts rule that "Only a reasonable expectation of confidence is required."

Thes rulings may create a tort law regarding the misuse of private information; an example includes a 2014 case against Google for working around cookie blockers to obtain personal information for targeted ads (Vidal-Hall v. Google Inc.)

#### Defamation

Also known as libel or slander, this refers to the publication or voicing of statements that negatively affect the claimant's reputation. The concept is rarely applied in cases of information theft because the statements themselves must be false; true statements act as a defence. In addition, there is government pressure to reduce such cases (e.g. withdrawal of Legal Aid).

Defamation charges have been used in the past to prevent 'kiss and tell' stories from former employees. 

#### Injunctions and Super-injections

Injuctions can be made to prevent publications; these are the only actions that can be issued against persons unknown, as shown by the case of *Hampshire Waste Service v. Persons Unknown* (2003), summarized below:

- The case arose as a result of the *Global Day of Action Against Incinerators 2003.*
- Members of the Onyx group of companies, who own the main large waste incinerator sites throughout the country, faced the likely risk that one or more of their plants would be a target of an invasion by trespassers styling themselves as environmental protestors. 
- The experience of such global days of action in previous years had led to them suffering seriously damaging and costly invasions.
- In the preceding year, just one invasion alone at a plant in the course of construction had lead to legal and enforcement costs of ??120,000, not to mention the other consequential losses that had been experienced.
- All of the evidence clearly disclosed a case for an interim injunction, subject only to the potential problem that the claimant companies could not name even one protestor who would be involved.
- Notwithstanding this, the Onyx companies successfully applied for an injunction from the Vice-Chancellor, who was willing to grant the first injunction of its type against *persons unknown* to the context of trespass and protest demonstration situations.

Super-injunctions forbid both the public disclosure of information on a particular issue and any disclosure of the existence of the directive itself. However, both types of injuction are only applicable within UK jurisdiction.

##### Mareva Injunctions (Asset freezing orders)

If a person who has stolen information is identified, rapid action is often required. A Mareva injunction freezes assets at short notice, and is intended to prevent the dissipation of assets before court judgment. They are named after the second case to grant them: *Mareva Compania Naviera SA v. International Bulkcarriers SA* (1975).

Mareva injunctions do not transfer the ownership of assets; it merely prevents their use or movement.

#### Anton Piller orders (Search orders)

These are search warrants that do not require a warning, but are orders where the defendant must give permission for searchers to enter. They are generally used when a search is required at a very short notice (e.g. to prevent the destruction of computer data). The name is derived from *Anton Piller KG v. Manufacturing Processes Limited* (1975) - a case that dealt with the theft of trade secrets.

Anton Piller orders are very destructive to targeted businesses, as they reveal important business information to others, and computers may be seized and kept for months. As a result, there is an extremely high threshold for their issuance:

- There must be an extremely strong *prima facie* case against the repsondent
- The damage, be it potential or actual, must be very serious for the applicant
- There must be clear evidence that the respondents have in their possession relevant documents or things and that there is a real possibility that they may destroy such material.