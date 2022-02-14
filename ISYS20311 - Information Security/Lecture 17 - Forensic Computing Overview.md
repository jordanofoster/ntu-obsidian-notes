# Forensic Computing Overview

## Key Concepts
- Digital investigations are conducted for a number of reasons:
	- Securing computer systems
	- Criminality/legal compliance
	- Information management
- IT facilitates both the commission and investigation of the events in question.
	- Technology enables new types of crime, and the means to investigate those crimes.
- Digital investigations should be carried out in a way that allows any resulting evidence to be presented in court.
	- There can be a conflict between doing it right and doing it fast.
	- The primary solution to this is to carry out investigations on non-persistent forensic images, rather than the original computer.
- Evidence should be presented in a legally valid and compelling manner.

## What is Computer Forensics?

*"\[Computer Forensics is\] the application of computer investigation and analysis techniques to determine potential evidence."* - Li & Seberry (2003).

The field focuses on investigation and analysis of systems to determine the responsibility for an event (or set of events). Forensic specialists follow clear, well-defined methodologies and procedures, but have to be flexible when faced with the unusual or unexpected. Activities they perform with data include:

- Identification
- Extraction
- Preservation
- Interpretation
- Analysis
- Documentation

### Where and What?

Computer forensics is used both by law enforcement and organisations. The concerns for each are different:

#### Common concerns for law enforcement
- Unauthorised access to computer resources
- Monitoring/capture of network traffic to steal user IDs, passwords and other sensitive information.
- Use of digital equipment for criminal activities (encrypted emails, crime-related documents, etc).
- Computer/network activity of known criminals (murderers, paedophiles, etc.)

#### Common concerns for organisations
- Unauthorised use of data and information (leaks, 'stealing' trade secrets)
- Use of computer resources for non-work related purposes
- Breach of organisational policies (e.g. viewing pornography)
- Lax security on organisational machines

## National Security

Computer forensics is increasingly important for national security procedure, including detection of the following:
- Hostile intelligence collection
- Sabotages
- Terroristic plans

National Security focus is typically on protection of infrastructure; especially control rooms, such as those for power plants, rail transport, or water services. Stuxnet is an example of a case study on why this is important.

## Computer Crime

Old crimes are easier over time for non-experts, such as credit card fraud, embezzlement, blackmail and stealing. New crimes become possible, however, such as hacking or Denial of Service (DoS) attacks.

The following is one way to classify a computer crime, but it is not mutually exclusive:
- The computer, or the information on it, is the **target** of the crime - with the aim of damaging its integrity/confidentiality/availability (see [here.](https://www.bbc.co.uk/news/world-asia-23324172))
- The computer is a **respository** for information used/generated in the commission of a crime (see [here.](https://www.bbc.co.uk/news/magazine-20237564))
- The computer is a **tool** for committing the crime. (see [here.](https://www.bbc.co.uk/news/uk-england-hanpshire-18536940))

### What are the most common crimes/incidents?

The diagram below, provided by the 2018 Cyber Security Breaches Survey, shows this information:

![[Pasted image 20220214162111.png]]

## Forensics in law enforcement

Criminal activity will nearly always leave some electronic evidence on a computer, be it used as a respository, or as a target/tool. If the latter is true, evidence must be assembled:
- It must be:
	- Identified
	- Preserved
	- Analysed
	- Presented

There are many obstacles to computer forensic analysis, as computer evidence is inherently mutable:
- It can be readily altered/deleted
- Invisibly/undetectably altered
- While being altered, files can appear to be copied/actually copied (temporarily)
- Evidence can be stored in a different format to that which is printed/displayed

As such, computer evidence can be hard to separate from other data, and must be interpreted.

### FBI Handbook

The FBI's *Handbook of Forensic Services* identifies the following types of computer examinations and recovery procedures:
- Content
- Comparison
- Translation
- Extraction
- Deleted data files
- Format conversion
- 