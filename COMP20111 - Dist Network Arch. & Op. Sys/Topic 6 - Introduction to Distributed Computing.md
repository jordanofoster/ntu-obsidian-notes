# Introduction to Distributed Computing

## Computer Stack

From this point onwards, we will be looking at distributed applications and middleware built on top of a compute cluster.
![[Pasted image 20220112111647.png]]

## Converting our world from analogue to digital
When engineering parts of today's digital and highly distributed world, the following must be considered:
- Communication
	- And the infrastructure to enable it
- Complex systems & Software Services
- Emerging fields including quantum computing and other advancements such as decentralized computing

### Communicating

One of the main questions for a systems engineer is how to enable the communication and flow of data between people and devices. The internet is comprised of many networks that are linked via a number of key pipelines, that connect geographical areas. Engineers need to determine how best to manage and allow these networks to grow, and continue to efficiently transmit information. This includes consideration of the following:
- Aspects of infrastructure
	- Such as networking switches, cables, radio (wireless), bandwidth, security, etc.
- Protocols, old and new
- Scalability of our implementations
- Software systems
- Provided services

This is by no means an exhaustive list and there are many other factors to consider.

### Complex Systems

Large interconnected networks are naturally extremely complex, and as a result we must consider how to offer additional benefits and services to them. 

To provide an example, networked computers act as the enabling technology for large-scale computing, which involves a large number of computer nodes. These nodes can also be used to provide cloud functionality.

A complex software layer is required to allow these nodes to act together as a single entity, and abstract them as such to other developers. Thus, the following design issues are raised:
- How do we design and write the software that controls nodes as a distributed cluster?
- What specialised applications do we use our clusters for?
- What software layer(s) are required for enabling these systems for use?

### Cloud-based Systems

Systems engineers frequently find themselves working for companies that provide some form of cloud presence, or services based on the technology. They must ask themselves how these types of systems are engineered, and what they must consider for the following aspects of the process:
- Hardware
- Networking
- Topology
- Software Systems
- Virtualisation
- Security

### Large-Scale Computing Systems

#### Data Centres
![[Pasted image 20220112112832.png]]
A typical data centre server floor will have several racks, each of which containing 80 computers; the rooms themselves will also accomodate for the power and network cabling requirements. Generally, fibre-optic cabling is used to provide high-speed connectivity. These are the yellow wires shown in the below image:

![[Pasted image 20220112112851.png]]

Another important aspect of data centres is dealing with the vast amount of data that is generated and stored by the cluster when providing various services. For example, if each server on a rack has 2TB of disk space and at least 5120 servers are present in each data server, a minimum of *10,240TB* of backup space is required.

Keep in mind that this already large number does not include the additional storage requirements provided by data centres, such as index and document servers (using Google as an example).

Backups are required in the case of failure so that this information can be restored; The systems contain enough data that automated robotic systems are used to load tapes (the typical form of *cold* storage used in enterprise) into the backup devices.

Security is naturally a large concern during this process, as without necessary protections, data can easily be stolen by an adversary if the data centre itself does not have enough physical controls and measures undertaken.

## Design issues for building large-scale computing clusters

There are a number of these to consider when creating a High Performance Cluster (HPC) or mainframe. They are as follows:
1) Does this follow a mainframe design (with few processors but high bandwidth I/O), or is it built out of lots of smaller computers?
	- Which architecture (Mainframe or HPC) is best to use must be considered.
2) Are machines based on *multi-processor* or *multi-computer* architectures?
3) Which networking topology is used to link everything together?
4) How do we pass information between each component of the system?
5) How do we logically and physically organise and control system resources?
6) Do we use shared memory systems?
7) Do we use shared file systems?
8) What security issues must we consider?

Alongside these there are many more considerations to make.

## Types of Parallel Computer Architectures

![[Pasted image 20220112113653.png]]

The image above demonstrates a few examples of *tightly coupled* architectures (with on-chip parallelism, being *multi-processor*) and *loosely coupled* (*multi-computer*) systems.

### Multi-computer Topologies

![[Pasted image 20220112113823.png]] ![[Pasted image 20220112113827.png]]

Multi-computers can be connected in a number of ways, as seen above. There are some key things to consider:

- *Nodes* (**dots**) in topologies represent *switches* - or to be more exact, CPUs connected to switches.
- Each node can have a number of links to other nodes (*fanout*).
- The *diameter* of an interconnected network represetns the largest number of links that need to be traversed between the two most distant nodes. The *lower the amount of hops, the better.*
- The maximum bandwidth between nodes must also be considered.

## Other Distributed Systems: Internet of Things

Complex systems and products are now integrated into the home and office. The Internet of Things (IoT) is an extension of *Pervasive Computing* in which small devices are IP-enabled and connectible via internet.

As a result, we can start to integrate computing resources into devices to enable new things that we had not considered before, such as:
- Intelligent spaces (the environment changes and adapts based on our interactions with it)
- Using devices to help the elderly, or provide general healthcare
- And many more uses.

## Other issues to consider

There are even more issues we must consider when building robust distributed systems, such as:

- *Infrastructure Types*
	- Centralised/Decentralised computing
	- Cloud, Cluster & Grid-based computing
	- Plus physical networking and throughput, optimisted routing, etc.
- *Research Challenges*
	- Heterogeneity, Openness, Security, Scalability/Load Balancing, Failure Handling, Concurrency, etc.
- *Models* (Interaction, Failure, Security)
- *Messaging systems* and *decentralised coordination* and *IPC*
- File and Memory Systems
- *Clocks* and *synchronisation,* and the methods/algorithms for achieving this
- *Coordination* & *distributed* synchronisation methods/algorithms
- *Scheduling strategies* and methods
- *Virtualisation,* including principles, types, and hypervisor technology
- *Designing* effective software solutions
- *Data,* *Storage* and *Security*
	- The latter including *storage, transmission, protection and use*
- Programming distributed systems (using Java)

## Programming Distributed Systems

### Typical, Single-system Programming
![[Pasted image 20220112114707.png]]

When designing systems to run on a single machines, all functionality is considered to be offered as part of a single product; all functionality is implemented in one or more programs, and all will be running on one machine. This can be complex, but is generally fairly straightforward - with these considerations:

- All elements of the program are stored/executed on the local machine
- The program is stored/executed within a single addressable space
- The program might have access to other CPUs on the local machine
- Might be multi-threaded, and therefore requiring knowledge on concurrency and synchronisation
- Program might have to access network
- And typically will have a GUI/text interface.

### Distributed Programming

When designing a distributed system, multiple computers will be used, and thus functionality must be spread over different machines, by dividing up aspects of the software into different programs (running on different machines) to provide the *overall* desired functionality.

Instead of calling methods, we use a messaging system to get other machines to do something, and generally distributed programs do not have a user interface (excluding occasaionally on a head node).

Using coursework 1 as an example:

![[Pasted image 20220112115228.png]]

#### Java Crash Course - JDK, JRE & JVM

![[Pasted image 20220112115331.png]]

##### Edit-compile-debug cycle

![[Pasted image 20220112115626.png]]

When programming for complex systems, a program cannot work on the first build. We instead start by writing the code (*edit phase*), compiling it (*compile phase*), use the outcome to determine code/runtime errors (*debugging phase*) and then repeat the cycle until the program is correct.

##### What is a compiler?

![[Pasted image 20220112115714.png]]

Most programs, such as C, C++ and Java, will use one of these to *compile* source code (something *you* understand but the system does not) into something the processor can understand.

### Object-Oriented Programming (OOP)

Java is an Object-Oriented language. This is similar to C++, C# and Python. In real life, things are looked at as objects; a tabl