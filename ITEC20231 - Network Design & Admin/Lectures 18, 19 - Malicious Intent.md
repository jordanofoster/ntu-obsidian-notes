# Malicious Intent

The assumption is made that any organisation or individual with computers is a target for malicious intent, and that some attackers will be specifically targeting you, whereas others will just see you as a resource to exploit (targeted vs. dragnet attacks).

Methods of attack can be many and varied, as can attackers. Specific threats will be discussed only in as much as there are specific strategies to counter them. The security in practice module (year 3) will go into exploiting and defending against attacks.

## Dangers in Security

Concentration on a few known threats can leave targets vulnerable to those unconsidered. Targeting specific vectors is not enough, and an overall security programme has to be devised. Security itself may have to be handled by a sysadmin already overloaded with day-to-day tasks. They may be tempted to either lock everything down, or allow easy access to avoid hassle.

### Types of security concerns

There are a number of security concerns a sysadmin has to be aware of, such as:
- Coding errors (some):
	- Buffer overflows
	- Trapdoors (not an error, but someone adding extra code to circumvent security)
- Attacks (some):
	- SQL Injection
	- Dictionary Attacks
	- DDOS attacks
- Viruses
- Rootkits
- Spyware/Malware

The question is what sysadmins can do to help protect against these.

#### Example of a 'false target'

- [The top 25 types of coding errors](http://cwe.mitre.org/top25/)
- [A full CWE list of 1000+ problems](http://cwe.mitre.org/data/index.html)
	- This includes eveything from SQL injection (CWE-89) to improper access control (CWE-285).
	- 'Errors' here range in scale from coding bugs, to an overall failure to architect security structure.
	- As a result, it may tempt managers to concentrate *only* on those indicated issues.
		- Many of these errors are moreso symptoms of a bigger problem, such as sloppy coding standards, inadequate testing regime or a lack of managerial control.

See [Software \[In\]security: Top 11 Reasons Why Top 10 \(or Top 25\) Lists Don't Work](http://www.informit.com/articles/article.aspx?p=1322398)

#### SQL Injections
[As explained by xkcd.]([xkcd: Exploits of a Mom](https://xkcd.com/327/))

More seriously, though, the point of this comic strip is that any application may be considered vulnerable, unless proven otherwise. Microsoft has been quoted as saying that ["Perfect Security is Impossible".](http://msdn.microsoft.com/en-us/library/ft0y04t6(vs.71).aspx) A holistic approach must therefore be taken.

#### Command Injection

The code below shows how a simple Python program for copying a file to another destination can introduce a potential exploit:

```
import os
systemCommand = "cp"
srcFile = input("Please enter the name of the source: ")
dstFile = input("Please enter the name of the destination: ")
systemCommand += srcFile + " " dstFile
os.system(systemCommand)
```

Calling `os.system` will get the OS to execute the command given. This can be a problem:
- `"readme.txt + readme2.txt"` is fine.
- `"readme.txt readme2.txt;" + "rm -rf/"` is not!
	- This copies the file and then recursively deletes all files on the filesystem.
		- Sure, access control/authorisation can help reduce this; but what if SU/root did this?
			- Files would be deleted until the system was broken so much that it could not even do that!

#### Buffer Overflows

![[Pasted image 20220221165050.png]]

The above images show the following:
- (a) is a situation when the main program is running.
- (b) shows the situation after procedure A is called.
- (c) shows a buffer overflow in grey.

(For additional investigation; Stack Smashing, Metasploit, and [other penetration tools](https://sectools.org))

#### Trapdoors
```
# (a): Normal code with no security exploits

def login():
	name = password = ""
	while True:
		name = input("Login:")
		password = input("Password:")
		v = check_validity( name, password )
		if v:
			break
	execute_shell(name)

# (b): Code with a trapdoor inserted

def login():
	name = password = ""
	while True:
		name = input("Login:")
		password = input("Password:")
		v = check_validity( name, password )
		if v or (name == "clarkkent"): # Trapdoor
			break
	execute_shell(name)
```

for `(b)`, we can see that when checking whether the username and password is valid (stored in `v`) the next line introduces a trapdoor to see if the result is a valid set of credentials, *or* if the username is the same as `"clarkkent"` - this would circumvent our password security check!

#### [Dictionary Attacks](http://www.sci-tech-today.com/news/Data-Breach-Offers-Lessons-for-CIOs/story.xhtml?story_id=13300EUMKOJ4)

```
Set WinHttpReq = CreateObject("WinHttp.WinHttpRequest.5.1")
WinHttpReq.Open "POST", "http://www.domain.com/login", false
WinHttpReq.SetRequestHeader "Content-Type","application/x-www-form-urlencoded"
WinHttpReq.Send("login=Chris&password=Pa$$w0rd")
```

Dictionary attacks are a form of brute-force attack; we connect to a server many times a second, and send words from a dictionary as the password. Problems can arise here due to poor security policies on a server, such as:
- The account lockout duration has been disabled
- Password complexity requirements

#### Distributed Denial of Service Attacks (DDOSes)
![[Pasted image 20220221171025.png]]
These are done by flooding the server with Internet Control Message Protocol (ICMP) packets, such as (ping, syn, etc.)

## Security Tools

There are a variety of security tools to help in the defense of networks, which can be broken down into two types:
- Intrusion Protection
- Penetration Testing

Examples of tools include:
- NMap
- Nessus
- Snort
- etc.

For cracking/exploiting systems, some examples include:
- Metasploit
- John the Ripper

As stated before, check [sectools.org](https://sectools.org) for open source/free tools.

## Security Policy

How do we protect our servers within our network, or those that are accessible remotely? Are there any ways to minimise the risk of intrusion?

Security policies are the answer. You can adopt a policy based on the following:
- Perimeter security
- Defence in depth
- Security through Obscurity

### Perimeter Security

Perimeters require multiple layers of security, rather than one. For example, a [DMZ](https://en.wikipedia.org/wiki/DMZ_%28computing%29) is often used; the principle being that access to important services is protected. Only less critical services (those that *have* to use the internet) live in the DMZ. The direction of initiation of transactions is from the protected region, out via the DMZ.

#### [Examples of DMZ Topologies](http://technet.microsoft.com/en-us/library/cc778219.aspx)
![[Pasted image 20220221171842.png]]
- Use proxy servers within the DMZ to provide a single route for internet access.
- Keep services for databases and email private.
	- Use a separate set of servers within the DMZ to access them instead.
- We can use a reverse proxy to allow external users access to internal services.
- We *never* put a domain controller within a DMZ.

#### [Bastion Servers](http://www.securitysoftwarezone.com/how-bastion-hosts-work-review136-7.html)
![[Pasted image 20220221172112.png]]
These are used to host the services that sit inside the DMZ. Because of likelihood of attack, they are locked down as much as possible:
- No access to network files
- Logging is activated and the Bastion is monitored
	- Potentially, dual logging is performed via a separate dedicated machine
	- Unused services are removed.
	- No user accounts are present.
	- Intrusion detection software is installed.

### Defence in Depth

Assume that the system has multiple points of failure, and attempt to address all points of weakness, through methods such as:
- Virus checkers
- Firewalls
- Malware detection software
- Encryption
- Physical barriers

#### Design for Security

- The physical design of the network needs to ensure defensivfe layers, such as DMZs and firewalls.
- The logical design (i.e. in terms of corporate structure) needs to ensure separation of more/less important data.
- Simplicity of design should ensure that systems and software is easier to maintain, update and monitor.
- Documentation should aid maintenance, review and response to attack.
- Education of users is fundamental to reducing attack potential.

#### Question what you are buying

Sysadmins are expected to conduct due dilligence when purchasing equipment:
- What is the MTTF (Mean Time To Failure)?
- What is the maintenance service like?
- Has the supplier been accredited by ISO9000 or some other scheme?

A similar level of diligence should be used for software - especially if it is web based:
- Has the supplier been accredited to ISO9000 (and other standards)?
- What security process do they follow?
- What is their update/patch management like?

#### Software Suppliers & Security Policies

Suppliers should indicate which methods they use for quality software building. They should also have a process for ensuring security in tandem with basic quality standards, such as:
- [Microsoft Secure Development Lifecycle (SDL)](http://technet.microsoft.com/en-us/library/cc778219.aspx)
- [Comprehensive, Lightweight Application Security Process (Clasp)](http://www.newscientist.com/blog/technology/2007/04/seeing-through-walls.html)
- [[Electronic Eavesdropping Risks of Flat-Panel Displays.pdf|Software Security Touchpoints]]
- Suppliers should know how their software would fit into an ISO27001 system.

### [Security through Obscurity - A simple principle...](   http://history1900s.about.com/library/photos/blywwiip187.htm)

In wartime, the *need-to-know* principle was applied at all levels in society, through propaganda as seen below:
![[Pasted image 20220221173511.png]]

People were forbidden to access information by default; this must be considered as a potential policy when setting up groups and folders.

#### Another simple principle - *"If in doubt, leave it out"*

In our context - unless known to be necessary, *remove* things!
- Remove/disable default/built-in accounts (such as Guests) as general containers.
- If you want access to a website to be limited, configure IIS Security (e.g. force use of username/password credentials).
- Limit access to files/programs offline - disable caching too.
- Limit physical access (e.g. to servers/routers).
- Limit access to printers (especially those printing using special forms).

### Other Security Issues

- Active Directory
- Password and Login attempts
- Physical visibility
	- Can someone see what's being typed?
	- What about audio?
- Electrical visibility
	- see [[Lectures 18, 19 - Malicious Intent#TEMPEST http www newscientist com blog technology 2007 04 seeing-through-walls html and Attacks|]]TEMPEST.

#### Physical Devices

Key loggers cannot be detected, except through visual inspection:
![[Pasted image 20220221174057.png]]

We could also use handheld devices for unique password generation.

#### [TEMPEST](http://www.newscientist.com/blog/technology/2007/04/seeing-through-walls.html and) Attacks

![[Pasted image 20220221174254.png]]
![[Pasted image 20220221174301.png]]

These involve using the unavoidable emissions of computer systems to exfiltrate data, and are the main attack vector against airgapped systems. Intelligence agencies such as the NSA invest lots of money into these as they are cutting edge, so a high threat model is generally assumed. Vectors can include:

- Sound
	- Recording sound (speakers can be turned into microphones)
	- Playing ultrasonic sound to transmit data (speakers)
	- The noise several components make can leak data:
		- Hard drives
		- Fans
			- PSUs, Computers
- Light
	- Photon emissions (as seen above) from screens
	- Optical data transmission (morse?)
- Heat
	- The heat emanations from components can be altered to exfiltrate data.
- Electromagnetism
- Electricity itself
	- Data can be read/inferred from the fluctuations in a power line (from the PSU).