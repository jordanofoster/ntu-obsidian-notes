# Lessons Learned

Lessons are learned from experience of previous breaches about which practices would have (or did) improve the outcome of the situation.

## Motivation for reflection

- Encouraging 'best practice'
	- This refers to an agreed or assessed excellent practice that produces better results than other (known) approaches.
- Disseminating these best practices across infosec workers
- Facilitates the archival of knowledge as a result.

## After Action Reviews

Once an incident has been dealt with, several steps are required to make sure the same incident does not occur again. The first of these is the holding of an *After Action Review*, where lessons learned from past successes and failures are captured.

These aim to follow a 'no-blame' culture; that is, a mentality of blaming processes rather than people. The results of after action reviews are not always documented as a result, to maintain this idea.

AARs themselves ask the following questions:
- What was *intended* to happen
- What *actually* happened
- *Why* it happened
- *What*  was learned?

### Holding an After Action Review

An AAR should be held immediately after the incident is resolved, while all participants are still available and have fresh memory of it. AARs themselves should create the right climate for discussion, by following the right principles:

- AARs should have a culture of openness and commitment to learning ('doing better').
	- As such, they are free from the concept of seniority/rank, and are explicitly *not* critiques or evaluations of personal performance.

AARs should have a facilitator appointed; their role is not to 'have' answers as to what happened so much as to help those in session 'learn' the answers found. The event itself should be divided into discrete activities, each of which should have an identifiable objective and plan of action.

Discussion always begins with the first activity or question of 'What was *intended* to happen?' participants should first universally reach an agreeable conclusion about the facts of what happened during the incident, and then the plan the organization had is compared with what happened in reality. This consists of the following two steps:

1) Identify and discuss the successes and shortfalls of the actual procedure followed.
2) Put in place new action plans to sustain these successes and improve upon the shortfalls.

These key points should be recorded.

 ## Incident Walkthrough (Example 1)

 For the purposes of this section, we will use an example incident where unauthorised access to a computer system was obtained by someone using a 'stolen' set of credentials (login/password).

 Firstly, the incident is divided into discrete activities:
 1) Perpetrator(s) obtained legitimate log-in credentials for user *X.*
 2) Perpetrators logged in remotely using a VPN.
 3) Perpetrators downloaded various files
 4) Perpetrators did not delete nor (apparently) damage any files.

### "What happened?" (Example 1)

- User X says he has only used his credentials to log into the system at home and at work, *except for the update message.*
	- "*What* update message?"
	- X and numerous others received an urgent email from the sysadmin telling them of a security breach, and that they needed to update their passwords immediately.
		- X did this on Saturday morning from his home, using Outlook Web Access (OWA).
		- The sysadmin denies the sending of any such email.

### Revision of activities list

1) Perpetrator obtained the name of the sysadmin
2) Perpetrator sent fake (but convincing-looking) emails to numerous staff members
3) Perpetrator harvested login details from the staffs' responses.
4) X brings his laptop into the meeting - a check of the web cache shows access to an *unknown domain* on Saturday morning.

### "What happened?" Part 2: Electric Boogaloo

- An *Outlook Web Access* phishing attack occurred.
- The perpetrator obtained the name of the sysadmin from the corporate website.
- Perp cloned the company's OWA site, including graphics.
- Perp registered a lookalike mail domain in the form of *mailcorp.com* (instead of mail.corp.com)
- Perp sent emails purportedly from the sysadmin with a link directing the staff to the *fake* OWA site.
- After harvesting these details, the fake site redirected the users to the real site.

[A blog post explaining how this attack vector works is shown here.](https://community.rapid7.com/community/metasploit/blog/2012/01/19/simple-outlook-web-access-phishing)

## Phases of Improvement 

These are as follows:

1) Prevent the incident from occuring again.
2) Avoid hazards that caused the incident in the first place.
3) Improve the management system for crisis situations.

We will be using our [[Lecture 16 - Lessons Learned#Incident Walkthrough|prior incident walkthrough]] as a guideline.

### Prevent the Incident (Example 1)
- We remind employees to *never* give out their credentials by email.
- Additionally, we introduce a *new* policy:
	- *Employees should never give out sensitive information via OWA.*

### Avoid the Hazard (Example 1)
There are several options:
- Write a program to scan incoming emails for doubtful origin.
- We *stop* using OWA, and give employees a dedicated email client that works at home instead.
- We make use of two-factor authentication when using OWA.
	- E.g. sending a code to the user's phone (SMS 2FA)
	- This is a less draconian measure than banning OWA outright.
- Register our URIs (like *mail.corp.com*)
	- This is a good idea in general.
	- Introducing Mondays (?)

### Improve the Management System (Example 1)
- Create a telephone hotline for urgent username/password change requests.
	- Additionally, ban all requests by email.
		- This could be onerous if we have a lot of employees.
- Microsoft could mitigate this by adding *CSRF* (cross-site request forgery) tokens to the form authentication template in OWA.
	- However they didn't do it in Exchange 2010 - even though the problem has existed since *Exchange 2007!*

## Incident Walkthrough (Example 2)

*Three users of your dating website have complained that their accounts were hacked immediately after they set a brand new password.*

*The only common feature appears to be that all three logged in through shared computers in the same town: one in an Internet café, one in the public library and one over Wi-Fi in an upmarket café.*

Once again, we divide the incident into discrete activities:
1) Each user logged onto the dating website.
2) One purchased some credits; the other two already had sufficient credits in their account.
3) They all conducted a few searches, and sent a message (or two)
4) They all *explicitly* logged off
5) They all reported that these hacks occured on the *same day.*

### "What Happened?" (Example 2)

- Logs suggest that the logins themselves were valid.
	- So the login credentials themselves must have been stolen 

