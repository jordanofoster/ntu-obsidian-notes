# Cyber Attacks

Cyber attacks are of two kinds: **host** and **network** based.

## Host-Based Attacks/Controls

Host based attacks are run against a **specific system or machine,** such as laptops, desktops, etc. They aim to compromise the host itself and the information it contains, and this can **give further access to other hosts** depending on configuration. In large organisations, this vector is of particular concern, as security is only as strong as its weakest link - potentially thousands of hosts on a network provide many potentially unpatched systems.

### Malware 

Of main concern in host-based attacks is malware, a generic term for a **variety of malicious software** that can be installed on a host machine. This can include, but is not limited to:

- Viruses
- Trapdoors
- Trojan Horses
- Rootkits
- Spyware/Adware
- Worms

#### Viruses

Viruses are **self-replicating code** that embed themselves in host programs. They can use .exe files, macros in documents, or scripts on web-pages. Once installed, they will tend to carry out some other purpose such as deleting programs, encrypting data, or installing other malicious software. Viruses fortunately tend to have a unique signature, used by anti-virus programs to detect their presence - this tends to be in the form of hashes taken from a part of the program. As a countermeasure, then, some viruses **modify their own code** in order to avoid detection.

#### Trapdoors

Trapdoors are secret or undocumented methods of gaining access to an application, operating system or online service.

#### Trojan Horses

Trojan horses are malware that is **disguised as legitimate software** - they require user intervention to install. Installed trojans may then provide unauthorised access through trapdoors, disable security software, install other malware or hijack the machine to act as part of a botnet for the purposes of a denial-of-service attack.

#### Rootkits

Rootkits are a collection of tools that aim to provide admin access to machines or a portion of them thereof. As a result, they are often used to hide the presence of other types of malware, and are difficult to remove as they can subvert processes intended to catch them.

#### Spyware/Adware

These are software that collect usage data to send to a third-party, such as an advertiser or data firm. They can potentially track login data through tools such as keyloggers or through packet analysis - cookies also provide tracking of network use for this same purpose.

Adware tracks usage data much like spyware, but instead uses it to inject advertisements into the host machine's software in various ways.

#### Worms

Worms are malware that seek to replicate themselves through a network. Only the worm itself propagates; other malware, in this instance a *payload,* performs an attack itself and may include any of the above.

Worms themselves consume bandwidth and other network resources through their activity. An example is the Morris Worm of 1998 - a tool written to measure the size of the internet itself, accidentally causing a faster transmission rate than coded and thereby causing a form of unintended DoS attack.

#### Routes of Infection

Media tends to be the main method on which malware is distributed, such as CDs, DVDs, USBs, etc. As a result, organisations commonly disallow the use of external media. In the instance that it is actually neccessary, recommendations include the use of a *sheep-dip* machine to use this media on first (although this is impractical to do all the time).

Other methods include attachments over email, or websites users interact with. The introduction of *Bring Your Own Device* policies also provide a significant challenge.

### Network Attacks/Controls

Networks are the primary vector for attacks - infrastructure is used to threaten assets from geographically diverse starting points. Attacks include but are not limited to:
- Denial of Service (DoS)
- Network Eavesdropping
- Hacking/Unauthorised access
- Database/web attacks

#### Denial of Service

Refers to making an asset unavailable to authorised users and processes. It acts as a catch-all term for many types of attack, including but not limited to:
- SYN Floods
	- Exploiting the TCP handshake procedure when establishing connections
- Smurf attacks
	- Broadcasting a large number of packets using a victim's spoofed IP.
- DDoS attacks
	- Using botnets to carry out large scale attacks utilising a number of unique IPs.
- Application-layer attacks
	- Target specific services (application packets) instead of the network as a whole.
- Malformed packets
	- Exploiting vulnerabilities in protocol implementations, such as the *ping of death.* 

Many DoS attacks are difficult to defend against, as they are effectively just a brute force approach to damaging infrastructure.

#### Port Scanning

Port scanning involves probing a server for potential vulnerabilities. Tools that portscan do have legitimate uses for network engineers; *nmap* is a popular tool for finding open ports, active hosts, OSes and even applications that are currently being run. Another tool, *OpenVAS,* goes even further; scanning for known vulnerabilities from a *Network Vulnerability Tests* database.

#### Man-in-the-Middle Attacks

Attackers using this method secretly monitor and potentially alter information exchanged between two parties. There are a variety of techniques to do this:

- Packet sniffing
	- Monitoring/viewing network packets sent between parties.
- DNS hijacking
	- Used to redirect domain requests to the IPs of malicious webservers instead of the intended site.
- Session hijacking
	- Taking session tokens from previous logins to make requests of a site/service as a specific user.

###  Hacking/Unauthorised Access

The endgoal of many attacks is to gain unauthorised access to information. This can be through legitimate access portals (in the case of session hijacking) or through exploitation of design flaws - such as when attempting privilege escalation (going from user to root in a linux system through exploiting OS flaws, for example.)

### Database/Web Attacks

Many web attacks also seek to compromise existing databases, as they are valuable to businesses. Statistical attacks on larger datasets can also compromise the confidentiality of data subjects.
