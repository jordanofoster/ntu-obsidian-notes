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

Clusters can be built out of off-the-shelf commodities (e.g. a *Beowulf* cluster) or via specially designed nodes (e.g. *Blue Gene*). Clusters are interconnected nodes linked by high capacity networking, such as Ethernet (1Gbps) or InfiniBand (>30Gbps).

Middleware controls job allocation, file access, etc. Clusters themselves are viewed as a single entity, rather than the nodes being exposed as descrete computational devices.

Advantages of this type of computing include:

- 
## A quick word on Server Hardware

This typically differs from desktop-grade systems, as they contain multiple CPU sockets, a much larger memory capacity, higher-speed I/O (and networking) and support enterprise-class CPUs.

![[Pasted image 20220131132813.png]]







