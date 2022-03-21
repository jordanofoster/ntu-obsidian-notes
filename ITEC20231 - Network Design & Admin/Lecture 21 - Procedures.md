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