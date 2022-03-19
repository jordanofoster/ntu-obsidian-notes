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
1) Peers are *explicitly* aware of each other
2) The route to the other peer is known.

When the destination peer for a message is unknown, the message is piggybacked alongside resource discovery operations. All peers maintain direct routing tables with the addresses (hashed or plaintext) of other peers, allowing messaging to work efficiently (i.e. without the network suffocating from resource discovery messages).

The efficiency of P2P routing tables depends on the liveliness of the peers; as a result, listed peers are periodically pinged to check health and removed when no reply is received. This period is dynamically adjusted based on the relevant *churn* (i.e. the rate of peer joins/departures)

### Structured P2P Protocols
These include the following services:
- Chord
- Pastry
- Tapestry
- Kademila
- CAN, etc.

They are typically used for data discovery applications, where the structure of the topology aids efficient searching. Graphs of structured P2P topologies show small-world properties; that is, a path exists between any two peers, with a relatively small number of *edges*. Structured topologies often map out as ring structures with inbuilt shortcuts, forming a basis for scalable and efficient resource discovery and message passing.

Messages in most structured protocols are exchanged directly between two peers. If peers do not know each other, then *conduct routing* is required to determine the destination peer's location. To assist with this, an overlay lookup allows to steadily decrease the distance in address space from sender to receiver with every iteration of the lookup algorithm, until the destination address is resolved.

This recursive way of doing things turns out to be extremely efficient and scalable - once the lookup has successfully retrieved the underlay network address of the destination peer, then messages can be exchanged. There are variations on the lookup algorithm; these include iterative/recursive algorithms and/or parallelised queries (to a set of 'closest neighbour' peers).

### Hybrid P2P Protocols

Hybrid variants integrate elements of both structured and unstructured schemas with the intent of facilitating *both* discovery and dissemination of data. Prominent examples of hybrid protocols include file sharing services such as Napster, LimeWire and BitTorrent.

BitTorrent originally was a classically unstructured protocol, but has since been extended with structured features to provide a *fully* decentralised data discovery mechanism. As a result, BitTorrent was able to abandon the concept of "tracker servers" - which facilitated peer discovery in a centralised manner -  and thereby improve its availability.

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
These aim to compromise the availability or integrity of a P2P system. This includes the illicit denial of access or changing/deletion of data, thereby endangering functionality of P-DSs.

Whitewashing attacks are especially dangerous for reputation-based P2P systems, since they allow a low-reputation peer to leave the system and re-join as a new, benign user.

#### Routing Attacks
Routing attacks aim to compromise the availability/integrity of P2P networks, and play an important role in composite attacks - such as the Eclipse attack, which attempts to block a good node's view of the rest of the network. In these attacks, a malicious peer undermines the message passing mechanism, typically by dropping or delaying messages. 

Another variant is *Routing Table Poisoning* (RTP) - where an attacker deliberately modifies their own or another peer's routing tables  - for example, by returning bogus information to benign peer lookup requests.

Attraction and repulsion are specific variants of routing attacks that respectively increase or decrease the 'attractiveness' of peers, for example during path selection or routing table maintenance. Such attacks negatively affect P-DSs. A typical routing attack would include the compromise of Pastry's routing table, as it is often used in social networks.

#### Buffer Map Cheating Attacks
Through this vector, adversaries can decrease the availability of P2P networks - particularly those used for media streaming applications - by reducing the outgoing traffic load of their peers by lying to others about their data provisioning abilities when queried.

This also infringes on the integrity of the network, and affects P-OPs. As stated prior, this attack is extremely prevalent in P2P streaming services that rely on peer collaboration. BMC Attacks also imply several other issues, such as:
- Omission
- Fake Reporting
- Fake Blocks
- Incorrect Neighbour Selection

#### Sybil Attacks
These aim to compromise availability or confidentiality via the spoofing of P2P networks, and can be regarded as a specific type of node/peer insertion attack.

Sybil attacks insert into the overlay of peers that are controlled by one or more adversaries. This can happen at specifically or randomly chosen locations of the overlay topology depending on the aim of the attacker. 

Additionally, P2P applications consider system users as legal entities and as a result restrict the number of peers per user to the amount of allowed votes for that entity/person. As a result, imbalances occur as a result of the expected amount of peers per user being exceeded.

Sybil attacks also provide a good starting point for many attacks discussed prior as a result.

#### Eclipse Attacks
These decrease the availability, integrity and confidentiality of P2P networks by surrounding a good peer with a set of colluding malicious peers that collaborate to partially or fully block the good peer's view of the rest of the P2P system.

Having done this, an adversary can either mask or spoof the good node's external interactions through the malicious nodes. Eclipse attacks are composite attacks that may also involve the following other attacks:
- Routing Table Poisoning
- DoS/DDoS
- Sybil Attacks
- Collusion
- White-washing/censorship

As a result, Eclipse attacks affect both P-OPs and P-DSs.

#### Mitigation approaches:
It should be noted that the mitigation approaches described below increase P2P system resilience, but only until a critical mass of colluding malicious peers is reached.

Additionally, some of these mitigations involve cryptographic support or the identification of peers, which may interfere with application requirements, such as:
- Anonymity
- Heterogeneity
- Resource Frugality

##### Basic PoS (Proof-of-Stake) and P-DS Scenarios
Proper functionality of basic P2P protocol security mechanisms such as the following are key to threat mitigation:
- Authentication mechanisms
	- These help to maintain benign peer populations, and provide technical basis for downstream mechanisms, such as secure admission, alongside the following two mechanisms.
- Secure storage
	- This is vital for data centric applications to prevent illicit data modifications by malicious nodes.
- Secure routing

Their proper implementation allow allows downstream mechanisms to be implemented which may also further mitigate threat vectors.

##### Sybil/Eclipse Scenarios
Sybil attacks occur where attacks can begin with a small set of malicious peers and subsequently gather multiple addresses that allow those same nodes to give the impression of being a much larger cluster than they actually are.

Under Sybil attacks, LEAs (Localised Eclipse Attacks) can be launched with a chain of Sybil clusters. However, this assumes the existence of a singular path towards the victim that is attacker-manipulatable.

Alternatively, LEAs can be launched using Sybil peers - where mitigation relies on centralised authorities that handle peer enrolments or admission. By extension, adding certificates given by a common CA to peers' network IDs when they join the network is another option. 

Other mitigation techniques to prevent self-selection of network IDs by malicious nodes could include a signing entity that makes use of public-key cryptography.

##### Buffer Map Cheating Scenarios
Other disruptions can be used to attack the KAD P2P network, which is Kademlia based. This can be done by flooding peer index tables that are close to the victim node with false information, in a process that is a simple variant of a taLEA (Topology Aware Localised Eclipse Attack).

KAD network crawlers can be introduced to monitor network status and detect malicious peers during LEAs. This however results in large amounts of overhead, if each peer uses a mechanism to detect such malicious nodes - such that the approach becomes impractical as the size of the overlay network increases.

Divergent lookups have been proposed as an alternate mitigation of taLEAs; this is done where disjoint path lookups avoid searching the proximity of a destination peer, in order to skip wasting queries on malicious peers under the assumption that a taLEA is in progress.

##### Routing Scenarios
Mitigation mechanisms consider assigning multiple paths for each lookup, by using disjoint paths - this causes high message overhead, however.

Alternative options involve using cryptographic schemes to protect paths - but P2P, being designed around decentralised coordination, is a hard environment to implement centralised services within - as would be required to support the coordination of system-wide cryptographic signatures.


### Summarization of Attack Types
| Attack | Availability | Integrity | Confidentiality | Functionality |
| --- | :---: | :---: | :---: | :---: |
| Dos/DDos | Y | N | N | P-OP |
| Collusion | Y | Y | Y | P-OP |
| Pollution | N | Y | N | P-DS |
| White-washing/Censorship | Y | Y | N | P-DS |
| Routing | Y | Y | N | P-DS |
| Buffer map cheating | Y | Y | N | P-OP |
| Sybil | Y | N | Y | P-OP |
| Eclipse | Y | Y | Y | P-DS, P-OP |

The adversarial collusion of malicious peers is a key factor to launch attacks such as these. In many cases the inherent design of P2P (which foster scalability and fault tolerance) are exploited.

Attacks against P2P systems typically impact one of three factors of the system:
- Confidentiality
- Integrity
- Availability

Several of these attacks are known from other system architectures, such as client-server models, whereas others are new (unique to P2P systems) or new compositions of new and old attacks. 

The main difference from client-server architectures is that P2P overlays can grow very large, and adversarial efforts have to thus adapt accordingly, such as by scaling up the number of malicious peers. As a result, substantial coordination is required to execute collusion strategies effectively.

Such attacks vary depending on whether attacks have direct or indirect network access via the overlay. Indirect access methods require malicious nodes to properly join the network prior to the attack. This means that malicious peers have to announce their presence in the overlay network before adversarial behaviour can begin - thereby making these attacks very noisy.

## Distributed Systems and Coordinated Resource Clustering
### Distributed Concepts & Classes of Coordination
In contrast to the decentralised model of P2P systems, there are a multitude of distributed systems where interactions across resources and services are orchestrated using various coordination mechanisms; all of which provide the illusion of a logically centralised/coordinated system/service. This coordination can be in the following forms:
- Scheduler/resource manager
- Discrete coordinator
- Coordination group

These include ordering in time (causality) or varied precedence order across transactions in the distributed system.

### Distributed Concepts & Classes of Coordination

Distributed systems are a collation of geo-dispersed resources that collectively interact to provide the following:
- Services linking dispersed data consumers/producers
- High-availability via fault-tolerant replication, to cover resource (computing/communication) failures
- Alternatively, a collective aggregated computational/service capability to provide the illusion of a logically centralised/coordinated resource/service from distributed resources.

Distributed systems are also often structured in terms of services delivered to clients. Each service comprises of - and executes on - one or more servers, that clients invoke by making requests.

This could also be done on a single, centralised server, but the resulting service would only be as fault-tolerant as the server that hosts it (instead of several distributed servers).

In order to accommodate server failures, they are typically replicated - either physically or logically - to ensure some amount of independence across failures via isolation. As a result, replica management protocols help coordinate client interactions across these replica servers.

As a result of this approach, the handling of client failure/compromise - including their role in potential launching of attacks via malicious code - also needs to be considered.

### Systems Coordination Styles

In order for distributed resources and services to interact meaningfully, a basis of synchronisation - either in time or logical order - needs to be specified. This applies at both the network and process levels; at high-level, synchronisation types include the following:

###### Synchronous Coordination
All components of a distributed system are coordinated in time - as in lock step or *rounds*. Causality is explicitly obtained. 

Examples include typical safety-critical systems, such as aircraft fly-by-wire controls; where predictability and guaranteed real-time responsiveness is desired.

###### Asynchronous Coordination
Separate entities will take their steps in an arbitrary order, operating at different speeds. The ordering of events needs to be ensured via collective interaction. Typical examples include transactional systems, databases, web-crawlers, etc.

###### Partially Synchronous Coordination
Some restrictions here apply on action ordering, but no lock-step synchronisation is present; typical examples include SCADA control systems, or high-value transactional stock systems, where timeliness directly affects correctness of the service.

### Reliable and Secure Group Communication
Group communications involves various schema to ensure reliable message delivery (amongst the distributed entities). This can be in the form of simple point-to-point messaging supported by acknowledgements - such as ACK and NACK messages - to ensure reliable delivery.

Alternatives could include the use of reliable and secure multicast to provide redundant channels, or the ordering of messages alongside publish-subscribe forms of group communication. In such approaches, channels and messages can be encrypted or signed - though this incurs higher transmission and processing overheads.

Various other measures also fall into this category, such as:
- Credential management
- Symmetric/Asymmetric cryptography
- PKI Cryptosystems
- Secure key distribution

### Coordination Properties
A distributed system's utility comes from the coordinated orchestration of dispersed resources to yield collectively meaningful capabilities. These are the base definitions used:
- Consensus
- Group Membership
- Consistency

#### Consistency
Consensus refers to achieving an agreement on values, such as data or process IDs. it requires the following properties to hold:
1) Agreement. All good processes agree on the same value.
2) Validity. The agreed upon value is a good/valid one.
3) Termination. A decision is eventually achieved.

#### Group Membership
Membership is a key service property in distributed systems that determines several details:
- The set of constituent resources
- The nature of agreement achieved by valid participants:
	- Static,
	- Dynamic,
	- and Quorum membership
- And data.

From security perspectives, this often relates to integrity.

#### Consistency
There are two basic consistency models; strong and weak consistency models.

##### Strong Consistency Models
In these, participants must agree on one consistent order of actions to take. As a result, processes are guaranteed to reach consistency through determinism. Two popular models are:

- **Strict Consistency**
	- Here there are no constraints on the order of actions, so long as it is consistent to all participants.
- **Linearisability**
	- This is essential strict consistency, but with the additional constraint that the observed order of actions corresponds to their real-time order.

Strong consistency models are used in high-risk contexts, where any inconsistencies in data can lead to heavy consequences; in such situations, consistency of data is more valuable than availability, and strong consistency constraints result in more system delays (due to frequent synchronisation).

##### Weak Consistency Models

In these, participants do **not necessarily observe the same order of actions.** This can result in inconsistent states depending on the nature of constraints that observed actions must satisfy. These issues can be dealt with via conflict resolution mechanisms. Three popular options are:

- **Sequential Consistency**
	- Sequential consistency is met if the order in which actions are *executed* via a process are the same as their original order.
		- As such, the sequential *execution order* of every process is preserved.
- **Causal Consistency**
	- This is achieved by categorising actions into those that are causally related/dependent, and those that are not.
		- In this case, only the order of casually related actions need be preserved.
			- Two events are causally related if they both access the same data object, and at least one is a write event.
- **Eventual Consistency**
	- In eventual consistency, there are no special constraints that have to be satisfied by the order of observer actions.
		- The idea behind this is that participants will eventually converge to consistency;
			- Either by observing equivalent action orders or resorting to - albeit costly - conflict resolution mechanisms.

Systems with weaker consistency models became popular with the advent of the Internet - where wide-scale webservers had to accommodate large numbers of users. To achieve such demands, these systems sacrifice strong consistency for higher availability.

