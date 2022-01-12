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