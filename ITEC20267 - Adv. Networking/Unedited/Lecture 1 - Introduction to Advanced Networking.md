# Lecture 1 - Introduction to Advanced Networking

## Overview

Networks are used to interconnect many devices; this is done over both LANs and WANs.
For WANs:
- Since the telephone, circuit switching has been the dominant technology for voice comms.
- Since 1970, packet switching has evolved significantly for digital data comms. It was originally designed to provide a more efficient method than circuit switching for bursts of data traffic.

### Switched Communications Networks

Long distance transmissions between end devices are typically done over a network of *switching nodes.* They are not concerned about the content of data; their purpose being to merely provide a switching facility to move data from node to node until the end device (the data's destination) is reached.

In switched comms networks, data entering the network from a station/end device are routed to the destination through node switching. An example of a simple switching network is shown below:

![[SwitchedCommsNetworks.png]]

#### Switching Nodes

Switched nodes may connect to other nodes, or some stations/end devices. The network is typically partially connected between nodes (that is, a node is only aware of neighbouring nodes and not the entire network) - although some redundant connections are desirable for the purposes of reliability.

There are two different switching technologies in use. *Circuit switching* and *Packet Switching.*

#### Circuit Switching

In circuit switching, a dedicated comms path is established between two stations in an end-to-end fashion. This path is a connected sequence of links between nodes - on each physical link, a dedicated logical channel is also formed.

Communication over circuit switching has three phases:
- Circuit establishment, done link-by-link
	- Routing/resource allocation (FDM or TDM)
- Data transfer
- Circuit disconnect
	- Deallocate dedicated resources

It should be noted that switches must also know how to find the route to the destination. An example of a circuit switched network is shown below:

![[CircuitSwitchingDiagram.png]]

##### Properties of Circuit Switching

###### Inefficiency

In circuit switching, channel capacity is dedicated for the whole duration of a connection - if there is no data being transmitted, the capacity is being wasted.

###### Delay

There is a long initial delay when establishing a circuit, and after establishment information is transmitted at fixed rates with no delay other than propagation.

###### Developed for voice traffic

Circuit Switching is also used for data traffic, but for voice connections, the circuit has a high utilization rate because often one party or the other is talking (and therefore using capacity).

#### Packet Switching

Packet switching is designed to address the problems faced by circuit switching. It operates by transmitting data in small segments called packets - typically about 1000 bytes long. Longer messages are split into a series of packets, and each packet contains user data and some control information, which consists of:

- Routing/addressing info, to allow the packet to be delivered to the intended destination
	- This also allows the content of an IP header to be recalled.

On each switching node in a packet switching network, packets are recieved, buffered (stored briefly) and then passed to the next node. An example diagram is shown below:

![[PacketSwitchingDiagram.png]]

##### Advantages of Packet Switching

###### Line Efficiency

A single node-to-node link can be dynamically shared by many different packets over time. Packets are also buffered and transmitted as fast as possible, reducing wait time.

###### Data rate conversion

Each station connects to the local node at its own speed. This is in contrast to circuit switching, where connections can be blocked if no resources are free - packet-switched networks never block transmission, only delay it, even under heavy traffic.

###### Priorities usable

Nodes can prioritise packets and forward them first, meaning they experience less delay that their lower-priority peers.

##### Packet Switching Techniques

Stations break long messages into packets, which are sent to the network sequentially, one at a time. There are two approaches to routing this stream of packets correctly through the network and towards intended destinations;  via *datagram* or *virtual circuit.*

###### Datagram

With datagram methods, packets are treated independently and do not reference those before them - each node instead chooses the next node a packet travels to.

As a result, packets can take any possible route, and may suffer from various issues, including reaching the reciever out-of-order or going missing entirely. The reciever instead has the burden of re-ordering packets and requesting the re-transmission of those that are lost along the way.

Datagram transmission is frequently used as part of the internet.

![[DatagramDiagram.png]]


###### Virtual Circuits

In virutal circuits, routes are preplanned and established before any packets are transmitted - after establishment, all packets follow the same route.

Packets contain *virtual circuit identifiers* instead of destination addresses - each node on a pre-established route knows its relative position within the virtual circuit and where to forward the packets it recieves. As such nodes need not make routing decisions for each packet.

Examples of virtual circuit protocols include X.25, Frame Relay, and ATM.

![[VirtualCircuitDiagram.png]]

It should be noted that virtual circuits *do not* have dedicated resources reserved for them. Packets therefore need to be stored and forwarded.

### Comparison of Communication Switching Techniques

A tabular comparison is shown below:

| Circuit Switching | Datagram Packet Switching | Virtual Circuit Packet Switching |
| ----------------- | ------------------------- | -------------------------------- |
| Dedicated transmission path | No dedicated path | No dedicated path |
| Fast enough for interactive | Fast enough for interactive | Fast enough of interactive |
| Messages are not stored | Packets may be stored until delivered | Packets stored until delivered |
| The path is established for entire conversation | Route established for each packet | Route established for entire conversation |
| Call setup delay; negligible transmission delay | Packet transmission delay | Call setup delay; packet transmission delay |
| Busy signal if called party is busy | Sender may be notified if packet not delivered | Sender notified of connection denial |
| Overload may block call setup; no delay for established calls | Overload increases packet delay | Overload may block call setup; increases packet delay |
| Electromechanical or computerized switching nodes | Small switching nodes | Small switching nodes |
| User responsible for message loss protection | Network may be responsible for individual packets | Network may be responsible for packet sequences |
| Usually no speed or code conversion | Speed and code conversion | Speed and code conversion |
| Fixed bandwidth | Dynamic use of bandwidth | Dynamic use of bandwidth |
| No overhead bits after call setup | Overhead bits in each packet | Overhead bits in each packet |

#### Virtual Circuits vs. Datagram

##### Virtual Circuits

- Networks can provide sequencing (packets arrive at same order) and error control (due to retransmission between nodes).
- Packets forwarded more quickly based on virtual circuit identifier and less routing decisions to make.
- Less reliable as if one node fails all circuits that pass through that node also fail.

##### Datagram

- No call setup phase makes datagram good for bursts of data, such as webapp traffic.
- More flexible than virtual circuits; if a node fails, packets can find an alternate route, and routing allows packets to avoid congested areas in a network.

