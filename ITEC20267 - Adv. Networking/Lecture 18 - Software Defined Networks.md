# Software Defined Networks
Resources used:
- [What is SDN and where software-defined networking is going](https://www.networkworld.com/article/3209131/what-sdn-is-and-where-its-going.html)
- [What is Software-Defined Networking (SDN)?](https://www.vmware.com/topics/glossary/content/software-defined-networking)
- [Software-Defined Networking](https://www.cisco.com/c/en_uk/solutions/software-defined-networking/overview.html)

## What is a Software Defined Network (SDN)?
This is a network in which the control plane is physically separate from the data plane, wherein a single, logically centralized control plane controls several forwarding devices.

![[Pasted image 20220319201603.png]]

Before beginning, the following should be considered:

*Overall, the idea of a SDN feels unsettling to some, as it proposes the change of one of the main reasons for the success of computer networks: fully decentralised control. Once we introduce a centralized entity to control the network, we have to make sure that it doesn't fail, which is very difficult.*

SDNs have a heavy presence in many large networks, however - as demonstrated below by Google:

![[Pasted image 20220319201859.png]]

### Planes in SDN
The *Data Plane* handles the processing and delivery of packets with a local forwarding state:
- Forwarding state + packet header -> forwarding decision
	- Commonly used for filtering, buffering and scheduling of packets.

 The *Control Plane* handles computation of the forwarding state within routers; it determines how and where packets are forwarded, and is commonly used for a few things:
 - Routing
 - Traffic engineering
 - Failure detection/recovery, etc.

The *Management Plane* works with configuring and tuning the network, and sees use in the following:
- Traffic engineering (once again),
- ACL (Access Control List) configuration,
- Device provisioning, etc.

#### Timescales of SDN Planes
| | Data | Control | Management |
| --- | --- | --- | --- |
| Timescale | Packet (nsec) | Event (10 msec to sec) | Human (minutes-to-hours) |
| Tasks | Forwarding, buffering, filtering, scheduling | Routing, circuit set-up | Analysis, configuration |
| Location | Line-card hardware | Router software | Humans or scripts |

#### Data and Control Planes
![[Pasted image 20220319202459.png]]

#### Data Plane

Here we can apply streaming algorithms on packets by matching some header bits and performing some actions. An example is IP forwarding:

![[Pasted image 20220319202554.png]]

##### Illustration of Data Plane
![[Pasted image 20220319202736.png]]

#### Control Plane
Here we compute the paths the packets will follow, and populate forwarding tables. Traditionally, this is a distributed protocol - for example, in Link-state routing (OSPF, IS-IS), we flood the entire topology to all nodes, and each node computes the shortest paths via Dijkstra's algorithm.

##### Illustration of Control Plane
![[Pasted image 20220319202820.png]]

#### Management Plane
When undergoing traffic engineering, we must set node weights. There are several factors to consider:
- Should it be inversely proportional to link capacity?
- Should it be proportional to propagation delay?
- Should we instead perform *network-wide* optimisation, based on traffic?
![[Pasted image 20220319203012.png]]

### Why use SDN?
As seen prior, networks are hard to reason about, hard to evolve, and expensive:
- There are too many task-specific control mechanisms, with no modularity and limited functionality. 
- We have indirect control, and must invert protocol behaviour to "coax" it into doing what we want, for example by changing weights instead of paths for "TE"(?)
- Our control is uncoordinated, as we cannot control which router updates first
- Interacting protocols and mechanisms
	- Routing, addressing, access control, QoS

#### SDN Changed Networks
![[Pasted image 20220319211436.png]]

#### Software Defined Networks
![[Pasted image 20220319211530.png]]

The *Network OS* is a distributed system that creates a consistent, up-to-date network view, and runs on servers (controllers) in the network. Examples of Network OSs include:
- NOX
- ONIX
- Floodlight
- Trema
- OpenDaylight
- HyperFlow
- Kandoo
- Beehive
- Beacon
- Maestro, etc.

Network OSs use *forwarding abstraction* to get state information *from* forwarding elements and give control directives *to* forwarding elements.

![[Pasted image 20220319211730.png]]

#### Control Program
The control program operates on a view of the network; the input has a global network view via a graph/database, whereas the output allows to configure each network device. The control program itself is not a distributed system; abstraction hides the details of a distributed state from it.

#### Forwarding Abstraction
This provides a standard way of defining forwarding state:
- Flexible, as behaviour is specified by control plane, and it is built from a basic set of forwarding primitives.
- Minimal, as it is streamlined for speed and low power, and the control program is not vendor-specific.

OpenFlow is an example of such an abstraction.

#### Virtualisation in a Software Defined Network
![[Pasted image 20220319212024.png]]

###### Virtualisation Simplifies Control Program
![[Pasted image 20220319212122.png]]
![[Pasted image 20220319212132.png]]

### Does SDN Simplify the Network?
Abstraction does not limit complexity, as the network OS and Hypervisor are still complicated pieces of code. SDN mainly simplifies the control program interface instead (though this is user-specific) and pushes complexity into reusable code in the SDN platform, much like compilers.

### OpenFlow Basics
![[Pasted image 20220319212315.png]]
![[Pasted image 20220319212328.png]]
![[Pasted image 20220319212341.png]]

We must consider a multi-tenant data centre, as we want to allow each tenant to specify a virtual topology. This also defines their individual policies and requirements. The data centre's network hypervisor compiles such virtual topologies into a set of switch configurations by taking 1000s of individual tenant virtual topologies and computing configurations that can implement all of them simultaneously.

This specific functionality is what people pay for with SDNs, and is enabled by SDN's ability to virtualize the network.




