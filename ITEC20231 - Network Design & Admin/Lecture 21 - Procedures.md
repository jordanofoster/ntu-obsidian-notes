# Procedures
## Managing the Network
*Coping* is where administrators deal with individual situations from scratch, before they arise (even if they've happened before). *Managing* is where organizational needs have been analysed and procedures defined and used for the range of occurring activities - and at its best, has procedures in place to check and update procedures.

## Golden Rules of network administration
- If it isn't broken, don't mess with it
- When in doubt, reboot!
- Never ever change anything *late in the day.*
- Never ever change anything *on Friday.*
- Always be able to *undo* what you are about to do.
- If you don't understand it, don't mess with it on a production system; Use test systems for experimenting.
- Dedicate a system disk devoted only to the system software. Put applications on other drives.
- Projects are not done until tested by yourself and by end-users.
- Projects are not done until documented.
- All projects take twice as long as planned.
- Use default settings when possible.
- Do not roll out new software without training end users:
	- Roll out an employee's new application immediately after they have received training to reinforce what has been learned.
- If you're having to fight fires all the time, *find the source.*
- Avoid poor decisions from above.
- ***Backup***

## Procedures for what?
Procedures must be designed for the the following:
- Tasks regularly carried out (e.g. for preventative checking)
- Event driven tasks (where events occur naturally within an organisation's lifetime)
- Event driven tasks, but those very rarely carried out
	- But might be important when they are (e.g., disaster recovery)

### Regular Procedures
There are several types:
- Security log check/analysis
- System log check/analysis
- Specialist log checking (Printer, DC, DHCP)
- Backups (different types at different times)
	- If automated, then logs must still be checked
- "Walking the job"
	- Physical checking of security: room access, tampering, unknown devices
	- Physical checking of status: printer paper supplies, user machines

Some are less frequent:
- Performance monitoring
- Restoration testing
- Software update checking - testing, rollout
- Scheduled maintenance - setup and system restart
- "Ticket" analysis - what problem, who and why?
- Asset inventory (NIC, IP, OUI, etc.)
- Network auditing (much less frequent, may be done via external consultants)
- Network assessment
	- Not for faint-hearted management!

### Event Driven Procedures
Normal event procedures include:
- New user
- Departure of user (under normal notice)
- New client machines (migration, or for a new user)
- New or upgraded server
- Retirement of a client machine/server
- Movement of a user between groups/jobs
- Request for restoration of files
- Handling user help requests
- Handling fault reports

Non-normal event procedures include:
- Departure of user with extreme prejudice
- Departure of sysadmin (under a cloud)
- Faulty/dead hardware:
	- Client PCs
	- Servers
	- Network infrastructure
- Illegal materials discovered
- Security breach/attack, physical/logical
- Disaster declared

## Occasional Tasks
Some tasks may be so individual that a procedure is not worth it, but a *process* (higher level of description) is:
- Evaluating new potential hardware/software/vendor
- Setting up a new network/major upgrade to existing network
- Retiring old services/applications

All of these need a report/set of notes in the form of an analysis, reflection and correction style, however.

## Network Systems Methodology/Process overview
![[Pasted image 20220321174229.png]]
### Data In/Out of Network Analysis Stage
![[Pasted image 20220321174301.png]]
### Data In/Out of Network Architecture Stage
![[Pasted image 20220321174343.png]]
### Data In/Out of Network Design Stage
![[Pasted image 20220321174421.png]]

## Guidelines for writing procedures
All procedures should contain:
- The name of the task
	- Clearly identified
- Author, Date and Issue Status of procedure
	- As the procedure changes with time, we need to know this
- Skills/access needed to accomplish/technical grade
	- So the procedure is not attempted by those without skills/access necessary
- Checklist, to be completed and signed at the end of the procedure, then filed
	- Gives a record of individual steps and any problems
		- Sign