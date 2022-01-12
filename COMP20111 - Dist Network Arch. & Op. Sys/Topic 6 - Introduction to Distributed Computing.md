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

- *N