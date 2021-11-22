# Lecture 4 - Advanced Routing

`This lecture replicates online teaching material from Cisco.`

## Path Determination
When routers recieve IP packets over an interface, it determines which interface must be used to forward a packet to its destination - a process known as routing. The interface used may be the final destination, or a network connected to another router that works to reach the destination network. Each network connected to a router typically requires separate interfaces, but this is not always the case.

A router has two primary functions:
- Determine the best path to forward packets based on routing table information
- Forward these packets to their destination.

![[PathDetermination.png]]

### Longest Match

The best path in the routing table is also known as the longest match. The longest match is the route in the table that has the **greatest number of far-left matching bits** with the destination IP address of the packet, and is always preferred. 

Routing tables contain entries consisting of a prefix (network address) as prefix length. For a link to be made between the destination IP of a packet and a route in the table, a minimum number of far-left bits must match. The prefix length of the route is used to do this.

#### Example of IPv4 Longest Match

In the tables below, an IPv4 packet has destination IP `172.16.0.10`. The router has three entries in the routing table that match this packet - `172.16.0.0/12, 172.16.0.0/18, 172.16.0.0/26.` Of the three, `172.16.0.0/26` has the longest match and would be chosen for forwarding.

It should be noted that for any routes to be considered a match, the  number of bits that match must at least be that indicated by the subnet mask of the route.

| Destination IPv4 Address | Address in Binary |
| ------------------------ | ----------------- |
| `172.16.0.10` | **1010110000010000.00000000.00**001010 |

| Route Entry | Prefix/Prefix Length | Address in Binary |
| :---------: | -------------------- | ----------------- |
| 1 | `172.16.0.0`/**12** | **10101100.0001**0000.00000000.00001010 |
| 2 | `172.16.0.0`/**18** | **10101100.00010000.00**000000.00001010 |
| 3 | `172.16.0.0`/**26** | **10101100.00010000.00000000.00**001010 |

#### Example of IPv6 Longest Match

In the tables below, an IPv6 packet has destination IP `2001:db8:c000::99`. Three route entries are shown, but only two are a valid match - one of which, `2001:db8:c000::/48`, being the longest match.

The first entries match because their prefix lengths have the required number of matching bits. The third fails, because its `/64` prefix requires 64 matching bits.

| Destination IPv6 Address | `2001:db8:c000::99/48` |
| ------------------------ | -------------------- |

| Route Entry | Prefix/Prefix Length | Does it match? |
| :---------: | -------------------- | -------------- |
| 1 | **2001:db8:c0**00::**/40** | Match (40 bits) |
| 2 | **2001:db8:c000**::**/48** | Match (48 bits, longest) |
| 3 | **2001:db8:c000**:5555::**/64** | Does not match (64 bits) |

### Building a Routing Table

- **Directly Connected Networks** are added when a local interface is configured (with an IP and subnet mask/prefix length) and is active (up and up).

- **Remote networks** are those not directly connected to the router. It learns about them in two ways:
	- **Static routes**, which are added during manual configuration.
	- **Dynamic Routing Protocols**, which are added as routing protocols dynamically learn about remote networks.
	
-  The **Default Route** defines a next-hop router to jump to when the routing table does not already have an existing route to match the destination IP of a packet. It can be added manually or learned automatically, like how remote networks are added.
	-  Default routes have /0 prefix lengths, meaning no bits need to match with the destination IP for the route to be used - it is used if there are no routes with a match longer than it.
		- As a result, they are sometimes referred to as *gateways of last resort.* 

### The Packet Forwarding Decision Process
![[PktFrdDecisionProcess.png]]
1. A Data Link frame with encapsulated IP packet arrives on an ingress interface.  
2. The router examines the destination IP from the packet header, consulting the table.
3. The router finds the longest match.
4. Using the longest match, the packet is re-encapsulated into another data link frame and forwarded out the egress interface. This destination could be a device on the local network, or a next-hop router.
5. If no matching route entry is found and there is no fallback, the packet is dropped.

After the router determines the best path, one of the following is done:

###### Forward packet to device directly on network
If route entry indicates that the egress interface is part of a directly connected network, packets can just be forwarded directly to the destination device. This typically happens on Ethernet LANs.

To encapsulate a packet in the Ethernet frame, routers need to determine which destination MAC address is associated with the destination IP address of the packet itself. This process varies dependant on IPv4 or IPv6 being used.

###### Forward packet to next-hop router

This is done if the destination IP is determined to be on a remote network. The next-hop address is always indicated as an entry in the routing table.

If both the forwarding and next-hop router are on an Ethernet network, a similar process to direct device forwarding is used (either ARP or ICMPv6 Neighbor Discovery) to determine destination MAC address.

The main difference here is that the router searches for the next-hop router in its ARP table or neighbor cache, instead of checking the destination IP address. This process can vary for different types of Layer 2 networks, however.

###### Drop packet if no match made

If no match exists and no default route is defined, the packet is simply dropped entirely.

#### End-to-End Packet Forwarding

Packet forwarding functions are primarily responsible for encapsulating packets into the correct data link frame for the outgoing interface. For example, there are many different frame formats for a serial link:

- Point-to-Point (PPP)
- High-Level Data Link Control (HDLC)
- Or other Layer 2 protocols supported by the interface.

#### Packet Forwarding Mechanisms

The primary responsibility of a packet forwarding function is to encapsulate packets in an appropriate data link frame type for an outgoing interface. Routers more efficient at this task can forward packets faster. Three mechanisms tend to be supported:

- Process switching
- Fast switching
- Cisco Express Forwarding (CEF)

###### Process Switching

This is an older packet forwarding mechanism. When a packet arrives on an interface, it is forwarded to the control plane, where the router's CPU matches the destination address with the routing table, determining the exit interface and forwarding the packet onwards. This is done for every packet that passes through the router, even if the destination is the same for a stream of them.

![[ProcessSwitching.png]]

###### Fast Switching

This is another old mechanism that acted as a successor to process switching. Fast switching uses a cache to store next-hop details. When packets arrive, they are again forwarded to the control plane, but a match is first checked against the fast-switching cache. If it is not present, then process switching is used instead.

Flow information for a packet is stored in the fast-switching cache; if another packet going to the same destination arrives, that cached next-hop information is automatically used without requiring any CPU intervention.

![[FastSwitching.png]]

###### Cisco Express Forwarding (CEF)

This is the most recent IOS packet forwarding mechanism. A Forwarding Information Base (FIB) is built, alongside an adjacency table. Table entries are not packet triggered (like fast switching), but triggered by change instead (such as changes in network topology). When networks converge, the FIB and adjacency tables contain all information to consider when forwarding a packet.

![[CEF.png]]

### Basic Router Configuration

#### Topology

![[RouterTopo.png]]

The topology in the image above will be used to show various config and verification samples, and to discuss the IP routing table.

#### Route Sources

Routing tables contain a list of routes to known networks, containing prefixes and prefix lengths. This is sourced from direct networks, static routes and dynamic protocols. Sources for each route in a table is identified by a code. Common codes include:

- L - address assigned to router interface
- C - directly connected network
- S - static route
- O - dynamically learned network from another router (using OSPF)
- * - candidate for default route

##### Routing Table Principles

There are three principles, described in the table below:

| Routing Table Principle | Example |
| ----------------------- | ------- |
| Every router makes its own decision based on existing routing table info. | R1 only forwards packets that use its own table. R1 does not know of routes in other routers' tables (e.g. R2).
| The information in a table of one router does not neccessarily match another router. | Just because R1 has a route in its table to a network via R2, that does not mean that R2 also holds that knowledge. |
| Routing info about a path does not provide return info. | R1 receives a packet with destination IP of PC1 and the source IP of PC3. Just because R1 knows which interface to forward the packet over, doesn't mean it knows how to forward packets from PC1 back to PC3's remote network. |

##### Routing Table Entries

![[RouteTableEntriesDiagram.png]]

In the figures above, the numbers identify the following info:

- Route source (how the route was learned)
- Destination network (prefix + prefix length) - identifies address of remote network
- Administrative distance (Trustworthiness of route source. Lower values are preferred.)
- Metric (Identifies value assigned to reach remote network. Lower is preferred.)
- Next-hop (Identifies IP of next router to which a packet would be forwarded.)
- Route timestamp  (How much time has passed since route was learned.)
- Exit interface (Egress interface to use for outgoing packets to reach final destination.)

##### Directly Connected Networks

To learn about remote networks, a router must have at least one active interface configured, complete with IP and subnet mask (aka prefix length). This is a directly connected network/route - routers always add one of these when an interface is configured with an IP and activated.

Each is denoted by C in the routing table, containing a network prefix and prefix length. Local routes for each directly connected networks are also stored, indicated by L.

For IPv4 local routes, prefix length is /32; for IPv6, /128. The destination IP must therefore match all bits in the local route for a match to be made.

The local route's purpose is to efficiently determine when the router recieves a packet specifically for an interface instead of one that requires forwarding over it.

##### Static Routes

After direct interfaces are configured and added, static or dynamic routing is implemented for accessing remote networks. Static routes are manually configured, defining an explicit path between two devices - as such they are not automatically updated, and must be manually reconfigured if topology changes.

There are three primary uses of static routing:

- Ease of maintenance for the routing table in smaller networks with little-to-none predicted growth.
- Single default route to represent a path to any network without a more specific path. Default routes send traffic to any destination beyond the next upstream router.
- Routing to and from stub networks - networks accesses by a single route, with a single-neighbor router.

The topology in the image below is simplified to show only one LAN attached to each router; both IPv4 and IPv6 static routes are configured on R1 to reach 10.0.4.0/24 and 2001:db8:acad:4::/64 networks on R2.

![[StaticRouteDiagram.png]]

##### Dynamic Routes

![[DynRouteDiagram.png]]

Dynamic routing protocols are used by routers to share status/reachability information about remote networks automatically. They do this by performing several activities, including network discovery and maintaining the routing table.

In the sample topology above, OSPF is being used to dynamically learn all networks connected to R1 and R2. Status code **O** is used to indicate the route was learned via OSPF - both entries in the tables also include the IP address of the next-hop router via the *ip-address* command. It should be noted that IPv6 routing protocols use the link-local address of the next-hop router instead.

![[DynRouteDiagram2.png]]

##### Default Route

The default route specifies the address of a next-hop router that is used when there is no specific route that matches the destination IP of a packet. They can either be static or dynamically learned from a protocol. Default routes have an IPv4 entry of 0.0.0.0/0 or an IPv6 entry of ::/0, meaning no bits need to match between the destination IP of a packet and the default route for it to be considered a 'match'.

![[DefaultRouteDiagram.png]]

##### Structure of IPv4 routing tables

IPv4 was standardized using the classful addressing architecture (now obsolete). Tables based on IPv4 use the same structure - although lookup processes no longer use classes, the structure of the table itself still retains information in this format.

![[IPv4CMDEx1.png]]

Indented entries are known as child routes - indented entries are the subnet of a classful address (i.e. class A/B/C) - directly connected networks are always child routes, as the local address of an interface always has an entry of /32. A child route will contain the route source and all forwarding information (such as next-hop address). The classful address of this subnet is shown above the route entry, less indented and without a source code - known as a parent route.

##### Structure of IPv6 routing tables.

IPv6 never utilised classful addressing in its initial specification, so their routing tables are comparatively straightforward, as each entry is formatted and aligned the same way. 

### Administrative Distance

A route entry for a specific address (prefix/prefix length) can only appear once in a table, but a table can learn about the *same* address from more than one source. Excluding specific circumstances, only one dynamic protocol should be implemented on a rotuer, as each routing protocol may decide a different path to to reach the same route based on metrics of that protocol.

As a result, a few questions are raised; how does the router know which source to use, and which should it install in the table? 

Cisco IOS systems use Administrative Distance (AD) to determine which route to install. AD is a measure of route trustworthiness; the lower the distance, the more trustworthy the source. 

The table below lists various protocols and their associated ADs:

| Route Source | Administrative Distance |
| ------------ | :---------------------: |
| Directly connected | 0 |
| Static route | 1 |
| EIGRP summary route | 5 |
| External BGP | 20 |
| Internal EIGRP | 90 |
| OSPF | 110 |
| IS-IS | 115 |
| RIP | 120 |
| External EIGRP | 170 |
| Internal BGP | 200 |

### Should static or dynamic routing be used?

First, it should be noted that the two are not mutually exclusive, and that most networks use a combination of both. However, there are some differences:

#### Static routing uses

Static routes are commonly used for the following:

- As a default route to forward packets to a service provider
- For routes outside the routing domain, not learned by the dynamic protocol
- When the network admin wants to explicitly define a path
- For routing between stub networks

Static routes tend to be useful for smaller networks with only one path to outside networks. It also helps provide security in a larger network when it comes to certain types of traffic, or links to other networks that require more control.

#### Dynamic routing uses

Dynamic routing protocols are commonly used for the following:

- In networks that consist of more than just a few routers
- When changes in network topology require automatic determination of another path
- For scalability purposes; as networks grow, dynamic routing protocols automatically learn about new networks.

Dynamic protocols are implemented in larger networks, as they are scalable and automatically determine better routes when topology changes.

##### Comparison Table

The table below summarises the differences between the two:

| Feature | Dynamic Routing | Static Routing |
| ------- | --------------- | -------------- |
| Configuration complexity | Independent of network size | Increases with network size |
| Topology changes | Automatically adapts to topology changes | Administrator intervention required |
| Scalability | Suitable for simple-to-complex network topologies | Suitable for simple topologies |
| Security | Security must be configured | Security is inherent |
| Resource Usage | Uses CPU, memory and link bandwidth | No additional resources required |
| Path Predictability | Route depends on topology and routing protocol used | Explicitly defined by administrator |

### Evolution of Dynamic Routing Protocols

Dynamic protocols have been used in networks since the late 1980s. One of the first was RIP, with RIPv1 being released in 1988 - but some basic algorithms within the protocol was used in ARPANET as far back as 1969. As networks evolved and became complex, new protocols emerged.

![[EvoDynRoutingProtos.png]]

The table below classifies current routing protocols:

|  | Interior Gateway Protocols | Exterior Gateway Protocols |
| - | -------------------------- | -------------------------- |
|  	| Distance Vector - Link-State | Path Vector |
| IPv4 |  RIPv2, EIGRP - OSPFv2, IS-IS | BGP-4 |
|  IPv6 | RIPng, EIGRP for IPv6 - OSPFv3, IS-IS for IPv6 | BGP-MP |

Interior Gateway Protocols (IGPs) are those used to exchange routing information within a domain administered by a single organization. There is only one External Gateway Protocol (EGP) - BGP.

BGP is used to exchange routing information between different organizations, known as autonomous systems (AS). BGP is also used by ISPs to route packets over the internet.

Distance vector, link-state and path vector protocols refer to the type of routing algorithm used to determine the best path.

### Dynamic Routing Protocol Concepts

Routing protocols are a set of processes, algorithms and messages used to exchange routing information and populate the table with the best paths. The purposes of dynamic routing include:

- Discovery of remote networks
- Maintaining up-to-date routing info
- Choosing the best path to destination networks
- Ability to find new paths if current one no longer available

The main components of dynamic routing protocols includes:

- Data structures; 
	- Routing protocols typically use tables or database for operations - this is kept in RAM.
- Routing protocol messages;
	- Protocols use various types of messages to discover neighbour routers, exchange routing info, and other tasks to maintain accurate network information.
	- Algorithm;
		- An algorithm is a finite set of steps used to accomplish a task - routing protocols use them to facilitate routing information and to determine the best path.

Routing protocols mainly determine the best path/route to each network, to be offered to the routing table. If another routing source with a lower AD is not present, the offered route is installed.


#### Discovering the Best Path

Best paths are selected by protocols based on the values or metrics it uses to determine distance to reach a network. Metrics are quantitative values used to measure distance. The best path is that with the lowest metric value.

Many routing protocols use their own rules and metrics to build and update tables. The table below lists some common protocols and the metrics they use:

| Routing Protocol | Metric |
| ---------------- | ------ |
| Routing Protocol Information (RIP) |Uses *hop count* as a netruc, Each router along a path adds a hop to the count. A maximum of 15 is allowed. |
| Open Shortest Path First (OSPF) | *Cost* is used as a metric, measured as the cumulative bandwidth from source to destination. Faster links are assigned lower costs compared to slower links. |
| Enhanced Interior Gateway Routing Protocol (EIGRP)  | Metrics are calculated based on slowest bandwidth and delay values. Load and reliability are also potentially factored. |

##### Load Balancing

When routers have two or more equal cost metric paths available, they forward packets using both equally - this is kmown as equal cost load balancing.

- The routing table itself contains the single destination network, but multiple exit interfaces, one for each equal cost path. Packets are forwarded using the multiple interfaces listed in the table.
- If configured correctly, this can increase effectiveness and performance of the network.
- Equal cost load balancing is automatically implemented by dynamic protocols; with static routes, it is enabled when multiple static routes to the same destination network exist, using different next-hop routers.

It should be noted that only EIGRP supports *unequal* cost load balancing.




