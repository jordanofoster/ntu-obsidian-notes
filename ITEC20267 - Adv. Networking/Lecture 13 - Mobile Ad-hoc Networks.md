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
- Wireless network links continuously chan

