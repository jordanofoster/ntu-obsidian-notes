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

Security for these systems is nuanced; one viewpoint focuses on the security of the underlying concepts and mechanisms that 