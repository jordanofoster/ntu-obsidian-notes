#COMP20111-DNAOS/dist-computing-challenges
# Distributed Computing & Challenges

## Current computing paradigms

Generally, computers are thought of as single devices, as seen below:

![[Pasted image 20220131131304.png]]

Everyday devices fall under the *centralized* computing paradigm. This means that for each device, they have a local set of resources (memory, processor, I/O, graphics, storage). They are fully shared and tightly coupled, with unification achieved under one operating system.

## What is parallel computing?

In parallel computing, all processing nodes in a machine can be coupled in different ways; tightly coupled, with shared memory, or loosely coupled, with distributed memory (or clusters), as shown below:

![[Pasted image 20220131131904.png]]

## Distributed Computing

Distributed systems are made up from multiple autonomous computers; each has its own CPU and memory, and communication is done through a network. *Message passing* is used to exchange information - depending on topology and use, a distributed system could be used to form a cluster (*highly-coupled*) or cloud (*highly/loosely-coupled*); the latter can be centralised or distributed depending on purpose.

### Trends in Distributed Systems

Distributed Computing has been becoming significantly more relevant and important for users in the past decade, as they are found in the following areas:

- Client/Server computing
- P2P Computing
- Pervasive/Ubiquitous Computing
- Internet of Things
- Cloud/Fog/Edge Computing
- Grid Computing
- Cluster (HPC) Computing

#### Client/Server Computing

The paradigm itself has been around for a considerable time, but Client/Server systems tend to be distributed, comprised of autonomous computing nodes (servers) that are accessible via a network that offers a variety of services. Client computers interact with the server(s) and services.

![[Pasted image 20220131132536.png]]
![[Pasted image 20220131132551.png]]

#### Peer-to-Peer (P2P)

This provides a distributed model for networked systems; instead of clients and servers, nodes in P2P networks act interchangably as client and server, providing a decentralized model for controlling resources. Peers in a network are self organising, providing distributed control; Ad hoc networking connects them together.

The size and topology of a P2P network can change dynamically by peers joining and exiting over time. P2P itself is susceptible to a number of security attacks, such as Denial of Service and Identity attacks, alongside Poisioning.

![[Pasted image 20220131133404.png]]

#### Pervasive Computing

Another form of Distributed System is embedded/pervasive computing technology. Sensors and actuators are used and controlled by various autonomous computing devices; depending on the hardware used, specifications can be either limited, or systems can be fully discrete.

Devices can interact with background/infrastructure servers & services as well. There are also other considerations that mst be taken on board:

- Effective means of programming in restrictive systems
- Power saving/Power scavenging
- Communication (efficient use of wireless tech, power usage)
- Integration of sensors/actuators
- Intelligent Systems
- Security, Privacy, Sensing, Coordination, etc...

#### Internet of Things

Complex systems and products are now starting to be integrated into the home and office; the Internet of Things is an extension of Pervasive Computing, in which small devices are IP-enabled and connected by the internet. We can start to integrate computing resources into devices to enable new things that we had not considered before, such as:
- Intelligent spaces (the environment changes and adapts based on how we react with it)
- Using devices to help the elderly (or general healthcare)
- Many more...

Challenges IoT systems must face include:
- Billions of IP-connected devices
- Security, privacy & trust (lots of different solutions exists such as Hive, but all have limited/no notion of security)
- Middlewares for controlling/coordinating large scale collections of devices
- Heterogeneity of devices and software
- Programming small scale devices to work collectively.

#### Edge & Fog Computing
![[Pasted image 20220131141137.png]]


Edge computing is a distributed computing framework, where data analysis/procressing takes place at the point of creation, such as an IoT device. Data transformation and processing can occur at the point of creation too (such as the device generating the data). This has the following advantages:

- Improves latency between device and cloud/datacentre
- Faster analysis/response to deal with changes at that location
- Would be connected wirelessly/mobile (4G/5G) to infrastructure

Examples of this include:
- Smart city deployments
- Vehicular networks

Challenges that must be considered:
- Network/device security risks
- Latencies and bandwidth within the infrastructure
- Management of devices and resources

Similarly, Fog computing refers to when processing takes place *between* the edge and data centre.

#### Cloud Computing

Clients access a back-end system that contains a cloud of resources, such as servers and storage. The nodes within the cloud can work collectively or independently through the use of virtualisation technologies, and provide elastic services. Examples of cloud computing include:
- Infrastructure as a Service
- Software as a Service
- Platform as a Service
- Web services

Cloud computing suffers from similar security issues as Grid Computing, which will be covered in Topic 11 alongside general Cloud and Virtualisation technologies such as *VMware vSphere* (Hypervisor/cloud layer), *Microsoft Azure* (& *MS Hyper-V*) and Amazon Web Services (*EC2*).

#### Grid Computing

![[Pasted image 20220131141742.png]]

This brings together heterogenous computing resources such as Servers/Workstations/Clusters/Supercomputers/Databases/Storage (etc) to solve large-scale problems. Resources are leased by enabling software to link them globally, so grid computing makes use of available connected devices.

The main grid types are *Computational, Data* and *Service* grids. Examples include *TeraGrid* and *BOINC* (Berkeley Open Infrastructure for Network Computing). Security issues include:

- Resources (host/network security)
- Services (denial of service)
- Authentication/Authorisation
- Information (Integrity/Confidentiality)
- Management (Credential)

As before, this is explored in greater detail in Topic 11.

#### Cluster Computing

![[Pasted image 20220131142151.png]]


Clusters can be built out of off-the-shelf commodities (e.g. a *Beowulf* cluster) or via specially designed nodes (e.g. *Blue Gene*). Clusters are interconnected nodes linked by high capacity networking, such as Ethernet (1Gbps) or InfiniBand (>30Gbps).

Middleware controls job allocation, file access, etc. Clusters themselves are viewed as a single entity, rather than the nodes being exposed as descrete computational devices.

Advantages of this type of computing include:

- Increased processing speed, as multiple machines are working together
- Cost effectiveness, as these are cheaper to put together than super computers
- Resource availability through failure handling and over-provisioning.

Security issues include inter-node communication snooping and service distruptions such as DoS. Again, this topic is covered further in Topic 9.

## A quick word on Server Hardware

This typically differs from desktop-grade systems, as they contain multiple CPU sockets, a much larger memory capacity, higher-speed I/O (and networking) and support enterprise-class CPUs.

![[Pasted image 20220131132813.png]]

## Case Study: Google

![[Pasted image 20220131142355.png]]
![[Pasted image 20220131142420.png]]

As shown above, for any form of large-scale distributed system, several things must be considered:

1) The computing nodes - are they loosely or tightly coupled? Additionally, what is the performance of memory/processing/disk/networking?
2) Network topologies - How do we best connect the nodes (read: most efficiently)? How is information propagated throughout the network?
	`NOTE: Will be looked at in more detail in a future lecture.`
3) Communication Protocols
4) Load Balancing
5) Synchronisation of tasks and concurrency

## Challenges in Distributed Systems

There are a number of challenges within distributed systems:

### Heterogeneity

There are lots of varieties of computing devices and software - in other words, heterogeneity means a collection of various computers, networks and software. How can we provide an *even* set of these? Introduction of middleware typically exists to mask thse differences.

![[Pasted image 20220131143012.png]]

### Openness

In computing we have many types of devices, standards and communication protocols; we need to consider that these are produced by different companies, consortiums or other governing bodies.

Openness is defined under the *Oxford English Dictionary* as *"The quality or condition of being open"* - or alternatively, *\[The\] absence of dissimulation, secrecy or reserve".*

Open systems require key interfaces (hardware/software) to be published, so that others can use and expand them. When considering open distributed systems, we need standard communication mechanisms with open interfaces (i.e. published and freely accessible) on how to access shared resources.

Due to the heterogeneity of devices and software, standards need to ensure that these interfaces are tested and verified for use in an open system.

### Scalability

The number of resources contained within a distributed network can differ considerably, depending on the purpose of the system. For example: a small home network of pervasive devices vs. a large compute cluster.

A system is scalable if it can remain effective when dealing with an increase in resources and users.

### Failure Handling

![[Pasted image 20220131143540.png]]

We encounter failures in different situations. For example, a failure in software that is not caught will result in the program crashing - or a *total failure.* When considering multi-computer/service environments, failures are typically partial - meaning that part of the system could fail, but other parts would still be running.

There are a number of ways to handle a failure:

###### Detecting Failures

Naturally, we want to detect if a failure has occurred. For example, if you wanted to check whether a message sent between two computers has been corrupted during transmission, you would use a checksum. This would allow us to detect simple failures.

On the other hand, the question of how you would detect if a server node in a cloud is operational is more complex; therefore, we need a way of managing when failures could occur.

###### Masking Failures

If a failure happens, we can adopt the approach of either hiding or making the failure less severe. An example of making a fault less severe is when a message has to be re-transmitted if it does not arrive; an example of *hiding* a failure is using a mirrored raid array where data is written to both disks. Corrupt data on one disk is hidden, as data from the other is returned.

###### Tolerating Failures

We can pass failures onto the end user instead of dealing with it at a system level.

###### Recovery from Failures

How do we recover from a failure? One way is by roling back information into the last known good state. For example, database transactions can be rolled-back if incomplete, and restore points can be used when applying system updates.

###### Redundancy

This is self explanatory, and involves having backup hardware to go.

### Concurrent Access & Shared Resources

How do we protect shared resources so that only one entity has access to it at any one time (to enforce mutual exclusion)? To share between threads on a single computer, we can use semaphores and mutexes.

However, we face issues when applying this to a distributed system, as communication protocols and invocation (Remote Procedure Calls or Event Messages) to allow the calling of methods on remote nodes.

![[Pasted image 20220131144221.png]]

### Scheduling

Scheduling in distributed systems is a lot more complex than within an OS, as it must meet the following criteria:

- General - must not introduce restrictions on what can be done (jobs/applications/etc)
- Fairness - similar to OSes, need to ensure that no single user ends up using most or all of the system.
- Efficient - Resources need to be effectively managed to maximise performance.
- Dynamic - System needs to be able to alter resource usage and current loadings based on the state of the system.
- Transparent - the management of resources and processing are hidden from the user.

This is covered further in Topic 9.

### Transparency & Quality of Service

When accessing a large scale system, we want users or applications to only see the whole - rather than individual - components. Types of transparency include:

- Access transparency
- Location transparency
- Concurrency transparency
- Replication transparency
- Failure transparency
- Mobility transparency
- Performance transparency
- Scaling transparency

The quality of service refers to how well systems perform when under load. Ideally, systems need to be able to handle high workloads and still perform efficiently.


### Security and Trust

Information is a commodity which needs protecting, so that it is only used for the purposes of what the user intends. As a result, it is of high intrinsic value. When considering security in a distributed system, we need to think about it in the following terms:

- Confidentiality - protects the information and resources from unauthorized users (either locally or in transit). 
- Data integrity - ensures that information and resources are not altered or corrupted.
- Access control - protects against interference and unauthorised access to resources.
- Authorisation - requires a single secure access point for a user to access the system.
- Accountability - required to know who (user or entity) was responsible for failure (data provenance, etc).
- Non-repudiation - Entity cannot refute that something was done (e.g. access data, send message)

## Programming Considerations

Programming distributed systems requires us to consider the aforementioned challenges, whether they are tightly or loosely coupled. Consideration must be additionally taken for:

- Changes in programming style - no longer sequential, parallel processing must be considered.
- Communication - Need to go beyond networking protocols, and consider methods for inter-processor communication and messaging systems.
- Memory - What strategies are present for dividing the addressable space between multiple nodes.
- Scheduling/Concurrency/Synchronisation - Parallel programming on multiple computers, each with potentially multi-processor and multi-core configuration.
- Load balancing, and distributing workloads evenly between resources.
- Middleware, with functionality to offer an even environment for applications to run.

These considerations will be revisited in detail in future topics.



- Scalability
- Failure Handling
- Concurrent access & Shared resources
- Scheduling
- Transparency
- Quality of Service
- Security and Trust
- Programming








