# Distributed Computing & Challenges

## Current computing paradigms

Generally, computers are thought of as single devices, as seen below:

![[Pasted image 20220131131304.png]]

Everyday devices fall under the *centralized* computing paradigm. This means that for each device, they have a local set of resources (memory, processor, I/O, graphics, storage). They are fully shared and tightly coupled, with unification achieved under one operating system.

## What is parallel computing?

In parallel computing, all processing nodes in a machine can be coupled in different ways; tightly coupled, with shared memory, or loosely coupled, with distributed memory (or clusters), as shown below:

![[Pasted image 20220131131904.png]]

### Distributed Computing

Distributed systems are made up from multiple autonomous computers; each has its own CPU and memory, and communication is done through a network. *Message passing* is used to exchange information - depending on topology and use, a distributed system could be used to form a cluster (*highly-coupled*) or cloud (*highly/loosely-coupled*); the latter can be centralised or distributed depending on purpose.

#### Trends in Distributed Systems

Distributed Computing has been becoming significantly more relevant and important for users in the past decade, as they are found in the following areas:

- Client/Server computing
- P2P Computing
- Pervasive/Ubiquitous Computing
- Internet of Things
- Cloud/Fog/Edge Computing
- Grid Computing
- Cluster (HPC) Computing

##### Client/Server Computing

The paradigm itself has been around for a considerable time, but Client/Server systems tend to be distributed, comprised of autonomous computing nodes (servers) that are accessible via a network that offers a variety of services. Client computers interact with the server(s) and services.

![[Pasted image 20220131132536.png]]
![[Pasted image 20220131132551.png]]

###### A quick word on Server Hardware

This typically differs from desktop-grade systems, as they contain multiple CPU sockets, a much larger memory capacity, higher-speed I/O (and networking) and support enterprise-class CPUs.

![[Pasted image 20220131132813.png]]

##### Peer-to-Peer (P2P)

This provides a distributed model for networked systems; instead of clients and servers, nodes in P2P networks act interchangably as client and server, providing a decentralized 




