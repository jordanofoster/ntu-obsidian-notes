# Mobile Ad-hoc Networks

MANETs are defined as a collection of wireless mobile hosts forming a temporary network without the aid of any centralized administration or standard support services. Ad-hoc network terminology itself is dynamic; nodes enter and leave the network continuously.

There is no centralized control or fixed infrastructure to support network configuration, be it initial or revisionary. Example scenarios for MANETs include:
- Meetings
- Emergency or disaster relief situations
- Millitary communications
- Wearable computers
- Sensor networks

## Route Finding

When creating MANETs, we want to determine an optimal way to find the optimal networking routes. There are dynamic links between nodes in MANETs:
- Broken links must be updated when one node moves out of communication range with another
- New links must be formed when a node moves into communication range with another node
- Based on this new information, routes must be modified.

As such, the frequency of route changes are a function of node mobility.

### Conventional Routing Protocols for Wired Networks:

#### Distance vector routing

- Each router has a table giving the distance from itself to all possible destinations.
- Each router periodically broadcasts its table to its neighbours
	- Neighbors will update their table based on this information to ensure they are using the shortest route to reach each destination.
- To route packets, routers check their table to find the next hop to the destination.
- The tradeoff here is how often routing table are exchanged:
	- Too often results in a large amount of overhead, excessive bandwidth and computational resources used.
	- Too infrequent results in sub-optimal or invalid (stale) routes
	- Can send routing table updates whenever information in the table changes due to a new link or a broken link.

#### Problems with using Conventional Routing in MANETs
Unidirectional links
- A communicating with B does not always imply that B can communicate with A.
Redundant links
Redundant links
- In wired networks, only one or a small number of routers connecting two networks
- In wireless networks, there may be several "gateway" nodes between a source and sink due to wireless channel properties.
	- Several redundant paths may be generated
	- This is a waste of bandwidth, computation and storage

Periodic routing updates
- Cost of sending routing updates (bandwidth, energy) is much greater in a wireless network than in a wired network
- Routing updates required even if nothing has changed
- In highly-connected networks, routing updates may collide
- Mobile cannot enter a sleep state because they need to hear all routing updates; this wastes energy.

Dynamic nature of ad-hoc networks
- Wired networks are relatively stable 
	- Occasionally links go down/come up or congestion changes the cost of a link
- Wireless network links are continuously changing due to node mobilty and environmental conditions
	- Convergence to stable routes may be too slow to produce useful information information if routing updates are not sent often enough
	- If routing updates are sent too often, it wastes the battery of mobiles and channel bandwidth

### Routing Protocols for MANETs:

#### Route discovery and route maintenance
##### Route discovery
- Initial discovery of valid route from source to destination
- Source node can send a query for a destination node
- Only destination node responds to a query
- If the destination node is located in the source node's transmission range, the destination responds and a link is established
	- No periodic routing updates are needed
	- Approach must be extended to a case where the destination node is not in the source node's transmission range

Thus, we want an approach that is simple and efficient. One solution is to perform controlled flooding of the query:
- Nodes receiving the query will append their address to the route being recorded in the packet header and boradcast the updated packet to all neighbours
	- When a node receives a query, it checks to see if its address is already in the header (indicating the packet was already flooded by itself)
	- If the address is present, the node drops the packet
- Each query is labeled with a unique request ID
	- Each node keeps a cache with request IDs of packets it has already forwarded
	- Discards packets with request ID listed in node's cache
	- Avoids duplicate queries sent throughout the network
- Node only propagates first copy of each route request packet it sees

Typically, the source and destination will not be far away in an ad-hoc network.
- We can add a TTL (time to live) to route request
- Each node reduces the TTL by one when it propagates the request
- If the TTL hits zero, the route request packet is dropped

When the query reaches the destination:
- The destination sends a response back to the node from which it received the route request, using the route in the packet header (if available)

Additionally, route discovery information can be piggybacked onto data such as TCP connection packets. This reduces latency (e.g. start-up time for the TCP connection), but increases overhead (since packets are flooded throughout the network)

Intermediate nodes can cache routes they have discovered. These can be used if they want to send a packet to a node listed in the route, and reduces overhead in terms of number of route request packets required. Nodes can also operate in "promiscious" mode, which has it listen to all packets exchanged on the network, allowing it to cache the routes that are listed within the packets.

##### Route Maintenance

Nodes can determine broken links through the ACK/NACK responses included in most protocols. If the link is broken, the following options are available:
- Node that detects the broken link reports this information back to the sending node.
- Alternatively, node can try to fix the link by sending out its own route request to the destination.

If no ACK/NACK is present in the link-layer protocol, nodes can listen to the channel to determine if the next hop will transmit a packet or not. If the node does not hear the forwarding of the packet, it is assumed that the link is lost. Explicit routing acknowledgements can also be used to determine the state of links.

#### Proactive vs. Reactive Routing
##### Proactive Routing
Nodes continuously evaluate and update routes.
- Periodic updates
- Triggered updates - when a link changes
- Efficient if routes used often
- Large amount of overhead
- Similar to conventional routing protocols

##### Reactive Routing
Node evaluate and update routes only when they are needed.
- When a node has a packet to send, it checks to see if it has a valid route.
- If no valid route known, node must send out a route-request message to obtain a valid route (controlled flooding of the network)
- Data sent using valid route
- Efficient if routes not used often

#### Proactive Routing Protocols
Each node maintains consistent, up-to-date routing information in the form of a table with the next-hop to reach every node in the network. Changes in link state are transmitted throughout the network to update each node's routing table.

Proactive routing protocols include:
- DSDV: Destination-sequenced distance-vector
- CGSR - Clusterhead Gateway Switch Routing

##### DSDV (Destination-sequenced distance-vector)
Each node maintains a table with the following:
- All possible destination nodes
- Number of hops required to reach that node
- Next hop along the route to that node
- Sequence number

The sequence number is used to distinguish new routes from old routes. Updates to the routing table are transmitted throughout the network via two methods:
- "Full dump" routing updates
	- Via a large packet that contains all routing information
	- Transmitted infrequently, when little change occurs in existing links
- "Incremental" routing updates
	- Contains only information that has changed since the last update.

Route broadcast packets are transmitted containing the following info:
- Address of destination
- Number of hops to reach destination
- Sequence number of information
- Sequence number of broadcast packet

The route broadcast packet is used to update tables at intermediate nodes. If the sequence number of the update is the same as the sequence number of the information in the node's own table, the route with the shortest path is used; if the update is newer, the node replaces its own information with that of the updated route.

##### CGSR (Clusterhead Gateway Switch Routing)
This is a clustering multihop approach, where the clusterhead controls nodes in a cluster:
- Nodes within the cluster use CDMA-type SS code to avoid inter-cluster interference
- The clusterhead itself can control channel access

There is a clusterhead selection algorithm within the cluster:
- This can perform minimum cluster changes to reduce overhead (e.g. clusterhead only changed if it moves out of the cluster, or another clusterhead moves into an existing cluster).

DSDV is used as an underlying routing mechanism for CGSR.

CGSR as a process is as follows:
- Nodes send data to the clusterhead.
- The clusterhead sends data to "gateway" nodes.
- The gateway nodes route the packet to a new clusterhead.
- The packet goes in a chain of clusterhead -> gateway -> clusterhead until the packet reaches the destination cluster's clusterhead.
- Each node keeps a "cluster member table" that contains the clusterhead node for each mobile in the network.
	- Updates to this table are sent via DSDV.

#### Reactive Routing Protocols

Routes are created only when needed with these protocols, and they require "route discovery" and "route maintenance". Reactive Routing is also referred to as "source-initiated on-demand routing".

The goal of these protocols is to minimize the amount of overhead compared with proactive approaches, at the expense of latency in finding a route when needed. Reactive protocols are:

- AODV: Ad-hoc on-demand distance vector
- DSR - Dynamic Source Routing

##### AODV (Ad-hoc on-demand distance vector)
The protocol works as follows:
- A node needing to find a route to a destination broadcasts a route request (*RREQ*) to its neighbouring nodes.
- Neighbour nodes broadcast a RREQ to *their* neighbours until the destination is found, or an intermediate node has recent information about a route to the destination.
- Each RREQ is uniquely identified by the source's ID and a sequence number.
- Intermediate nodes keep track of which neighbour node the RREQ came from, in order to establish a valid reverse path.

When a route is found, the destination or intermediate node sends (over unicast) a route reply (*RREP*) back to the neighbour that gave it the RREQ request. Intermediate nodes set up routing information based on the nodes from which they receive the RREP packet. These routes contain timers, and will expire if left unused.

Route maintenance is achieved differently depending on the change. If a source node moves, a new RREQ is sent to the destination node. If an intermediate node moves, its upstream neighbour propagates a link failure notification message to the source node, so that the source node can then send a new RREQ packet to find a new valid route.

Additionally, "Hello" messages are used to inform nodes of their neighbours. This can be used to ensure the link is kept alive, and can contain information about a node's neighbours to give information about the network topology.

##### DSR (Dynamic Source Routing)
This is similar to AODV, but the entire route is maintained within the packet header. Intermediate nodes do not need to keep the routing information to route packets, and no periodic route advertisements are needed.

Intermediate nodes that propagate a "route request" append their ID to the "route record" in the packet header. When the packet reaches its destination (or a node with a valid cached route to it), a "route reply" is returned:
- If the route reply is from the destination node, send the "route record" in the "route reply".
- Otherwise is the node is intermediate, append the cached route to the destination node to the "route record" in the "route reply".

The "route reply" itself is returned along various paths depending on context:
- If there is a cached path to the source node, it follows that.
- If symmetric links are assumed, the packet travels the reverse route of the "route record".
- The route reply can also be piggybacked with a "route request" to the source node.

Route maintenance is achieved via the use of "route error" messages to propagate information about broken links. All cached routes with broken links are removed from the table.
- Nodes themselves can use promiscuous mode to listen to all traffic on the channel.
	- This allows them to update their route caches based on information from packets.
	- If the node knows a better route to the destination, a gratuitious "route reply" to the source can be sent.
- If an intermediate node determines that the next hop in a "route record" is unreachable, it can replace the route with a cached route instead.

#### Final comparison of proactive vs. reactive protocols

##### Proactive Approaches
- More efficient when the routes are used often
- Assures the routes are ready when needed
- Requires periodic route updates (acts as a form of overhead)
- Node mobility affects the entire network as part of routing updates.

##### Reactive Approaches
- More efficient when routes are used rarely
- Requires the node to first find the route before data can be transmitted.
- Periodic route updates are not required;
- Can have localized route discovery to help deal with the problem of node mobility.

Simulations by Carnegie Mellon University show the following:
- Reactive protocols can deliver many more packets that proactive protocols when the node mobility is high.
	- Proactive protocols by contrast have too many routing updates triggered, and the routes themselves cannot converge.
- Overhead of reactive protocols is dependant on node mobility:
	- DSR has less overhead than AODV, as intermediate nodes cache routes and thus fewer "route requests" need to be sent throughout the network.
- DSDV's overhead is constant due to its periodic updates.
- When the node mobility is low, DSDV perform far better than when mobility is high.
	- Although reactive protocols still have lower overhead and better packet delivery ratios.

##### Overall conclusions
- DSDV performs well only in low-mobility situations. Even then, its overhead is still high.
- DSR and AODV perform well regardless of mobility.
	- DSR has the lowest packet overhead.
	- If the overhead includes the packet header (overhead in bytes) however, AODV performs better than DSR as it has smaller headers.
	- However the header overhead may be less costly than the packet overhead due to the cost to obtain channel access, MAC/PHY headers, etc.

## Current Research in Routing for MANETs

- Hybrid proactive-reactive approaches
- Multicast
- QoS support
	- How can guarantees be provided in such a dynamic network environment?
- Resource-aware routing
	- Using metric besides shortest-path for routing decisions
	- Low power routing
	- Trying to avoid network partitioning
- Location-based routing.

### Power-Aware Routing
Energy is needlessly expended in the following areas with current routing protocols:
- Overhearing transmission of packets not intended for the node ("promiscuous" mode)
- Contention
- Overhead in route finding and route maintenance.

Promiscuous mode is still useful, however:
- Some protocols take advantage of the ability for nodes to overhear transmissions to other nodes to gather more information.
- This also improves routing, as more up-to-date routing information is obtained.
- However a *large* amount of energy is required to receive and decode the entire packet.

Contention itself also requires power:
- Channel sensing
- Ac