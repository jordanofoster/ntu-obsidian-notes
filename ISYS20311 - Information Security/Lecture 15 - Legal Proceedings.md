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

The EU-wide General Data Protection Regulation took effect on the 25th May 2018. It updates the Data Protection Act of 1998 - with the biggest change being a huge increase in fines; to show an example, under UK law TalkTalk was fined £400,000 - under GDPR, this fine would be predicted as large as £52 *million.*

##### Other changes under GPDR

Individuals must give 'clear and affirmative consent' to the processing of their data. A checkbox is adequate; anything less (read: silence) is not. IP addressses and mobile device IDs are unquestionably defined as personal data; their status was previously questionable under the Data Protection Directive.

Genetic and biometric data are classified as 'sensitive personal data.' There is a strong incentive to pseudonymise data sets - such data is still classed as personal data, but is exempted from various GPDR requirements. Encryption of data is also encouraged.

The 'right to be forgotten' established by the European Court of Justice (See *Google Spain v. AEPD,* 2014) has been extended towards a 'right to erasure' - it is no longer sufficient to remove a person's data from search results under a request; data controllers must now erase that data entirely. However if the data is encrypted, it may be sufficient to destroy the keys rather than undergo the prolonged process of ensuring that the data is fully erased.

##### Complying with GDPR

Text-based checklists are available, provided by various organisations including the Information Commissioner's Office, for organisations to use when preparing to comply to GDPR. To provide an examplem under Article 39:

*"Data Protection Officers are under a specific obligation to implement appropriate training. Although not an express obligation for organisations where DPOs are not required, we consider it to be almost impossible to demonstrate that an organisation is able to achieve compliance without policies settin"*