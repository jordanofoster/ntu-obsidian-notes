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

This critical area involves threats to the mechanisms that help coordinate resources (typically middleware protocols). This can include:
- Aspects of synchronisation
- Replication management
- Viewing changes
- Time/event ordering
- Linearisability(...?)
- Consensus algorithms
- Transactional commits.

### Data Security

Distributed systems are reliant on data through the following inputs:
- Data sourcing
- Data distribution
- Storage of data
- Usage of this data in services

The [[ISYS20311 - Information Security/Lecture 1 - Overview#CIA Triad|CIA]] triad directly applies to each element of the data chain (alongside the interfaces within it), and therefore threats to each are present in distributed systems:
- Confidentiality
	- Information leakage threats
		- Side channel attacks
		- Covert channel attacks
- Integrity
	- Compromise of data correctness
	- Violation of data consistency, as observed by distributed devices
		- This includes different types of consistency (over storage/transactional services):
			- strong/weak/related/eventual/etc. 
- Availability
	- Delay/denial of data access.

As a result, addressing data security in a distributed context requires the above threats to be mentioned across several areas:
- Resources
- Access control
- Data transportation
- Coordination services

Alongside data threats themselves (in the form of malware).

## Decentralised P2P distribution models
The design of P2P paradigms correlate with the [[Lecture 17 - Security in Distributed Systems#Classes of Vulnerabilities and Threats|application categories]] given prior.

As stated before, these constitute a decentralised variant of typically centralised distributed systems. Their popularity is due to the benefits they provide in scalability, decentralised coordination and low costs. There are four protocol types:
- Unstructured P2P
- Structured P2P
- Hybrid P2P
- Hierarchical P2P

Regardless of model, P2P systems typically combine the following 5 principles:
1) Symmetry of interfaces, as peers can seamlessly swap between client and server roles
2) Resilience to damage in the underlying infrastructure and to peer failures
3) Data and service survivability through replication schemes
4) Usage of peer resources at edge of networks, granting low infrastructure costs, providing scalability and decentralisation
5) Addressing the variance of resource provisioning amongst peers.

### Unstructured P2P Protocols

Unstructured protocols are mostly suited for large scale, continually scalable data dissemination. Programs that use unstructured P2P such as Freenet or Gnutella mainly use unstructured P2P to disseminate data for the purposes of censorship-free communication or filesharing. 

While peers themselves do not have any topology that links them, an implicit topology exists embedded within the physical infrastructure in the form of tree or mesh-like subgraphs; these allow for low latency message exchange (e.g. to address timeline requirements of data dissemination applications).

P2P systems communicate across peers via messages. Messaging passing may be direct (using an underlay network between two peers) - but this requires the following:
1) Peers are *explicitly* aware of eachother
2) The route to the other peer is known.

When the destination peer for a message is unknown, the message is piggybacked alongside resource discovery operations. All peers maintain direct routing tables with the addresses (hashed or plaintext) of other peers, allowing messaging to work efficiently (i.e. without the network suffocating from resource discovery messages).

The efficiency of P2P routing tables depends on the liveliness of the peers; as a result, listed peers are periodically pinged to check helath and removed when no reply is received. This period is dynamically adjusted based on the relevant *churn* (i.e. the rate of peer joins/departures)

### Structured P2P Protocols
These include the following services:
- Chord
- Pastry
- Tapestry
- Kademila
- CAN, etc.

They are typically used for data discovery applications, where the structure of the topology aids efficient searching. Graphs of structured P2P topologies show small-world properties; that is, a path exists between any two peers, with a relatively small number of *edges*. Structured topologies often map out as ring structures with inbuilt shortcuts, forming a basis for scalable and efficient resource discovery and message passing.

Messages in most structured protocols are exchanged directly between two peers. If peers do not know each other, then *conduct routing* is required to determine the destination peer's location. To assist with this, an overlay lookup allows to steadily decrease the distance in address space from sender to receiver with every iteration of the lookup algorithm, until the destination address is reeolved.

This recursive way of doing things turns out to be extremely efficient and scalable - once the lookup has successfully retrieved the underlay network address of the destination peer, then messages can be exchanged. There are variations on the lookup algorithm; these include iterative/recursive algorithms and/or parallelised queries (to a set of 'closest neighbour' peers).

### Hybrid P2P Protocols

Hybrid variants integrate elements of both structured and unstructured schemas with the intent of facilitating *both* discovery and dissemination of data. Prominent examples of hybrid protocols include file sharing services such as Napster, Limewire and BitTorrent.

BitTorrent originally was a classically unstructured protocol, but has since been extended with structured features to provide a *fully* decentralised data discovery mechanism. As a result, BitTorrent was able to abandon the concept of "tracker servers" - which facilitated peer discovery in a centralised manner -  and thereby improve its availabilty.

### Hierarchical P2P Protocols

Typically, all servers in P2P systems are considered equal in terms of the services they can provide, both as a client and server. Hierarchical protocols change this, as in some scenarios it can be advantageous. Hierarchical protocols include a layered design of both structured and unstructured overlays - peers themselves are further categorised based on the following:
- Bandwidth
- Latency
- Storage
- Computation cycles

The protocols provision these resources, with some "super" peers taking the coordinating role. Usually the category with the fewest peers represents the back-end of the hierarchy, whereas high-peer categories act as frontends that can process service requests, and only forward requests they themselves cannot resolve to the "back-end" peers.

This method of doing things improves lookup performance, and also generates less network traffic (via messaging). Furthermore, commonly requested content can be locally cached to reduce download delay.

## Attacking P2P Systems

There are two functional elements of P2P systems that need broad protection:
1) P2P Operations (P-OPs) that are accessible through the service interface, such as:
	- Discovery
	- Query
	- Routing
	- Download, etc.
All of this functionality pertains to the network level.

2) P2P Data Structures (P-DSs), accessible at either the network level or locally on a peer's host machine, such as:
	- Data stored in peer's routing table
	- Resources shared with other peers

The focus is on attacks against the P2P network infrastructure itself (e.g., Denial of Service or routing disruptions) and don't consider attacks prepared/conducted using P2P systems that harm non-P2P systems, such as *Distributed* Denial of Service attacks.

Most attacks exploit fundamental features such as message exchange based decentralised coordination, or the fact that each peer only has a partial (local) view of the entire system, by aiming to trick other peers by giving incorrect data or colluding to create partitions that hide aspects of the system from good nodes. Such example scenarios include:
- Misleading peers in terms of routing
- Taking advantage of access to resources
- Overcoming limitations in voting systems or games
- Hiding information in the overlay, among others.

### Attack Types:
#### DoS, DDoS & Disruption Attacks
These manifest as resource exhaustion by limiting access to nodes or communication routes. In P2P architectures, attackers aim to decrease the network service availability of the overlay by sending excessive messages to a specific peer set, thereby negatively affecting P-OPs. Examples of affected P-OPs include:
- The peer join/leave mechanism
- Other arbitrary P2P service aspects:
	- Damaging routing put/get options in the DHT.

Benign peers may also be impaired by an excessive maintenance workload; additional, both DoS and DDoS attacks can have negative impacts on bandwidth usage and resource provisioning, resulting in degraded services.

#### Collusion Attacks
These aim to compromise the [[ISYS20311 - Information Security/Lecture 1 - Overview#CIA Triad|CIA triad]] in regards to P2P networks. In collusion, a sufficiently large subset of peers can operate together to carry out strategies that target P2P networks to negatively affect P-OPs.

Typical collusion attacks attempt to override control mechanisms (such as those for reputation or trust management), or control provisioning. *Sybil* and *Eclipse* attacks are based on attackers colluding to create network partitions that hide system state information from good nodes.

#### Pollution Attacks

Also known as Index Poisoning, these compromise a P2P system's integrity and P-DSs by adding incorrect information, which can then be proliferated (resulting in service impairments) Examples of this include the typhoid adware attack where the attacker partially alters the content, e.g., by adding advertisement at a single peer that subsequently spreads the polluted content to other peers.

#### White-washing/Censorship Attacks

These aim to compromise the availability or integrity of a P2P system. This includes the illicit denialto data. 
