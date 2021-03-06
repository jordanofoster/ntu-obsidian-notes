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
		- Signed off by an admin AND a user if appropriate
- Special conditions to be followed (e.g., for Domain Controller) and rationale
	- To remind the admin that some machines need special care, and why
- Instruction sequence (related to checklist)
	- Sequenced instructions with any necessary precautions

## General checklists before any major change
Complete checks for [[Lecture 21 - Procedures#Backups Recovery disks RAID and images|the]] [[Lecture 21 - Procedures#Service packs Critical updates Security Updates|first]] [[Lecture 21 - Procedures#Antivirus|three]] and then perform a full backup, storing in a safe location. Use a PDA and/or calendar feature to remind oneself of these critical items.

### Backups/Recovery disks, RAID and images
1) Are operating system recover disks required (server/workstation)?
	- Have they been created recently?
	- Are copies placed in a safe location?
1) Are backup recovery disks needed?
2) Is a full backup made on a routine basis?
	- Has a verified, full backup been stored in a safe, offsite location?
3) Are daily incremental backups being made?
4) Do any other software packages require/allow recovery CDs?
	- Have they been created and stored in a safe location?
		- Antivirus/OS/Applications/etc.
5) Is RAID/disk mirroring enabled, and correct functionality verified?

### Service packs/Critical updates/Security Updates
1) Are the latest of these installed?
2) Is there a schedule for updating these items (e.g. Weekly/Monthly)?

### Antivirus
1) Installed and updated?
	- Recovery disks required?
2) Is automated scan enabled and running?
3) Are automatic download updates or push downs of updated DAT files available and configured?
4) Is there a schedule for updating these items? (Weekly/Monthly)

### Securing Systems
1) Secure physical access to servers
2) Enable BIOS passwords
3) Lock server room
4) Ensure battery backups are installed and working properly.
	- Is the power supply adequate for the number of devices plugged in?

### Software Licences
1) Verify and record all software licences in possession.
	- Are additional licenses required? Remember that sysadmins can be held liable for this!

## Example Procedures

### Network Inventory
- Rationale:
	- NIC MAC addresses are unique and provide good tracking of traffic. Different aspects of system provide redundant information for cross-referencing
- Author/Date/Issue:
	- M.J.Martin, 2004
- Skills/Access:
	- Admin capable of using Linux scripts
- Special Conditions:
	- Cisco IOS switches only, computer with Perl, SED, awk, sh, sort, date, diff and grep to conduct inventory. Need to download/compile domainscan.c and fping.
- Checklist:
	- List of all IP addresses, NIC Addresses, OUI and DNS entries to be produced.
- Instructions:
	- [See reference.](http://searchnetworking.techtarget.com/tip/1,289483,sid7_gci1035201,00.html)

### Departure of User
- Skills/Access:
	- Admin privilege
- Special Conditions:
	- None
- Instructions:
	1) Use User Security Pass to confirm identity of user
	2) Assist user to retrieve/delete any personal information on their desktop machine and in their email
	3) Set up mail forwarding to appropriate other staff member
	4) Archive existing email to server
	5) Disable Domain User account
	6) Remove desktop from all groups (to ensure does not access with cached credentials)
	7) Run script to check no local user accounts of same name on clients (more particularly their own desktop)
	8) Sign in any hardware e.g. USB sticks, mobile phones, laptops. 
		- Confirm admin access not locked out for these devices
	9) Sign in any security devices e.g. handheld PW generator, swipe card
	10) If using biometrics, disable entry in database for their ID
	11) Disable remote access to answerphone
	12) Document all steps and device IDs, and sign off with copy for user
	13) After 2 weeks, confirm with user's manager that all necessary file accessible on server and removed from client machines. Backup client machines and reformat/reinstall.
	14) Remove user account
	15) After 26 weeks, remove backup and archived mail.


