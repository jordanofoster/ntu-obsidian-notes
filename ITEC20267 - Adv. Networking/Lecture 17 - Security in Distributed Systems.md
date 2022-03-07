# Security in Distributed Systems

[[Distributed_Systems_Security_issue_1.0.pdf|Resource used]]

## Classes of Distributed Systems

### Peer-to-Peer (P2P)
These involve decentralised point-to-point interactions across distributed entities without a centralised coordination service, and untimed control is a prominent characteristic of such systems. Examples of peer-to-peer systems include:
- Distributed file/music sharing/storage systems, including but not limited to:
	- Kademila
	- Napster
	- Gnutella
- Wireless sensor networks and online gaming systems can also fall into this category.

### Coordinated clustering
This is done across distributed resources and services, and is best understood when divided into two subclasses:

 1) The coordination of resources
 2) The coordination of services.

Both will be utilised throughout this chapter; the spectrum of distributed systems include:
- Client-Server models
- n-Tier multi-tenancy models
- Elastic on-demand geo-dispered aggregation of resources
	- Layman's term - *clouds*. They can be:
		- Public/Private
		- Hybrid
		- Multi-cloud
	- They can also be used for a variety of transactional services:
		- Databases
		- Ledgers
		- Storage systems
		- Key Value Stores (KVSs).

Google, AWS, Azure and Apache's *Cassandra* are companies/services that offer access to this class of system.

Security for these systems is nuanced; one viewpoint focuses on the security of the underlying concepts and mechanisms in a distributed system where resources and services are dispersed. The other considers the use of distribution as a way to provide security itself. For example:
- The dispersal of keys, instead of using a centralised key store, or the use of VMs to partition/isolate resources and applications.

This lecture will focus on the former category (of 'securing a distributed system'); however the latter will also be discussed, given that dispersed security mechanisms typically execute on dispersed resources.

### Footnote about distributed systems
It is worth mentioning that distributed architecture is often layered, where each builds upon the services provided by the last and coordinated services are offered across the system. At the lowest levels, individual device resources are accesssed through the OS - distributed systems are assembled through the interactivity between different components/services on different devices.

Vertical interactions across the layers of a distributed system are supported by middleware frameworks that support different communication standards, such as [[Topic 8 - Messaging Systems#Message Passing Interface MPI|message passing]], [[Topic 8 - Messaging Systems#Remote Procedure Calls RPCs|Remote Procedure Calls (RPCs)]], distributed object platforms, [[Topic 8 - Messaging Systems#Publish Subscribe|publish-subscribe architectures]] and the Enterprise Service Bus.

With such services, decentralisation and coordination at each layer may differ, resulting in hybrid compositions of decentralisation/coordination patterns.

## Classes of Vulnerabilities and Threats
Vulnerabilities relate to the design or operational weaknesses that allow for a system to be compromised by an attacker. These include:
- Access/admission control and ID management
- Data transportation
- Resource management and coordination services
- Data security.

Threats reflect the [[Lecture 6 - Risk Assessment|potential or likelihood]] of an attacker causing damage or compromising the system, and is an end-to-end property of a system. As a result, vulnerabilities are broadly grouped based on the blocks of functionality that define a distributed system.

As a result, these 'blocks' and the operations they perform create the base threat/attack surface (area to exploit) for the systems themselves. At higher levels, attack surfaces relate to compromising the following:
- Physical resources
- Communication schema
- Coordination mechanisms
- Services themselves
	- The usage policies on the data services use.

### Access/Admission Control & ID Management

Access/admission control determines authorisation to use/access the following within a distributed system:
- Resources
- Users
- Services

This can also include sourcing data and read/write access to data over a service's lifetime. The potential threats and consequential attacks can include the following:
- Masquerading/spoofing identity to gain access rights
- Denial of Service (DoS) attacks to limit access
	- Through depleting computing resources and breaking communication channels
		- Leading to them becoming inaccessible even to authenticated users.

It should be noted that distribution of resources tends to give access controls more value; the increase of information transported to support access controls can also increase the attack surface of the system.

### Data Transportation

Network level threats here span the following:
- Routing
- Message passing
- Publish-subscribe related resource interaction
- Event-based response triggers
- General threats across the middleware stack

Attacks against this area can be passive (eavesdropping) or active (modification of data). A typical example of this is a Man in the Middle (MITM) attack, where an adversary inserts themselves between a victim's browser and the web server itself, establishing two separate connections. This allows the adversary to actively record messages and selectively alter data, all without alerting to suspicious activity (if the system does not require endpoint authentication i.e. via SSL certificates).

### Resource Management and Coordination Services.

This critical area involve