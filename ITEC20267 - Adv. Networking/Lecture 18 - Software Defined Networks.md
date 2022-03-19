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
As seen prior, networks are hard to reason about, hard to evolve a


