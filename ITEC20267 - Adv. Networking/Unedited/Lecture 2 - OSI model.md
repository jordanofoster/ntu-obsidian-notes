# Lecture 2 - OSI Model

## Reference Models

### OSI 7-Layer
| OSI Model Layer | Description |
| --------------- | ----------- |
| 7 - Application | Contains protocols used for process-to-process communications. |
| 6 - Presentation | Provides for common representation of the data transferred between applications layer services. |
| 5 - Session | Provides services to the presentation layer and to manage data exchange. |
| 4 - Transport | Defines services to segment, transfer and reassemble the data over the network. |
| 3 - Network | Provides services to exchange the individual pieces of data over the network. |
| 2 - Data Link | Describes methods for exchanging data frames over a common media. |
| 1 - Physical | Describes the means to activate, maintain, and de-activate physical connections. |

#### The Networking Layer
![[NtwrkLayer.png]]

##### Responsibilities of the Networking Layer

The networking layer is responsible for the following:

- To transport segement from sending to receiving host
- On the sending side, encapsulates segments into datagrams
- On recieving side, delivers segments to the transport layer
- Provides network layer protocols on every host/router
- Routers examine header fields constructed by the networking layer in all IP datagrams passing through it

![[RespNtwrkLayer.png]]

#### The Data Link Layer Structure

The Data link layer consists of two sublayers; Logical Link Control (LLC) and Media Access Control (MAC). The LLC sublayer communicates between networking software on upper layers, and device hardware on lower layers. The MAC sublayer is responsible for data encapsulation and media access control.

![[DataLnkLyrStruct.png]]

IEEE 802 LAN/MAN standards are specific to the type of network. (Ethernet, WLAN, WPAN, etc.)

##### Responsibilities of the Data Link Layer

![[RespDataLnkLyr.png]]

The data link layer is responsible for communications between end-device NICs. It allows protocols in higher layers to access the physical layer, and encapsulates Layer 3 IPv4/6 packets into layer 2 frames. It also has error detection and corrupt frame rejection capabilities.

###### Basic Functionality
Packets exchanged between nodes may go through various data link layers and transitions of medium. At each hop along a path, a router performs four basic Layer 2 functions:
- Accepts a frame from the network medium
- De-encapsulates the frame to expose the encapsulated packet
- Re-encapsulates the packet into a new frame.
- Forwards the new frame on the designated medium of the next network segment.

###### Data Encapsulation

![[DataEncapsulation.png]]

Encapsulation is a top down process in the OSI model; the level above performs its process, passing down the packet to the next level - this is repeated by each level until the packet is sent out as a bit stream to another node.

###### Data De-Encapsulation

![[DataDeEncapsulation.png]]

Data is de-encapsulated as it moves up the stack. When layers complete their processes, it strips off its own header in the packet, moving it up to the next layer for another round of processing. This repeats at each layer until at a point an application can process. It typically manifests as 5 different stages:

1) Recieved as a bit stream
2) Frame
3) Packet
4) Segment
5) Data Stream

#### Physical Layer

![[PhysLayer.png]]

Before network communications can occur, physical connections to local networks must be established. This can either be wired or wireless, but generally applies regardless of a corporate or domestic setting.

Network Interface Cards (NICs) are hardware that connect a device to a network; some devices have only one, while others may have multiple for different types of connection (Wired/Wireless, for example). It should be noted that not all types of physical connection offer the same performance.

##### Encapsulation in the Physical Layer

![[Pasted image 20211025011632.png]]

The process of encapsulation in the physical layer is as follows:

- Bits are transported across the physical network medium
- A complete frame is accepted from the Data Link Layer, whereupon it is encoded as a series of signals transmitted to the local media.
	- This is the last step in the encapsulation process across all network layers.
- The next device in the path recieves the bitstream and re-encapsulates the frame, using the output to decide what to do next.

##### Physical Layer Standards

Standards created for the physical layer address three crucial areas:
- Physical Components
- Encoding
- Signalling

###### Physical Components

Physical components refer to the hardware devices, media, and other connectors that transmit signals representative of bits, such as NICs, interfaces/connectors, cable materials and designs - which are all specified in standards associated with the layer.

###### Encoding

![[Encoding.png]]

Encoding converts bitstreams into recognizable formats for the next device in the network path; this is in the form of predictable patterns. Examples of encoding methods include Manchester encoding (shown above), 4B/5B and 8B/10B.

###### Signalling

Signalling refers to the method under which bit values (i.e. 0 and 1) are represented over the physical medium (light, RF, electricity, etc.) Naturally, the method used will vary depending on the medium itself, as seen below:

![[Signalling1.png]]
![[Signalling2.png]]
![[Signalling3.png]]

##### Physical Layer Bandwidth
Bandwidth refers to the capacity at which mediums can transfer data. Digital bandwidth refers to the amount of digital data that can be transmitted in a given timeframe (typically bits/second). Properties of the medium, current tech, and the laws of physics all play a factor in this.

###### Units of Bandwidth

| Unit of Bandwidth | Abbreviation | Equivalence |
| ----------------- | ------------ | ----------- |
| Bits per second | bps | 1 bps = fundamental unit of bandwidth |
| Kilobits per second | Kbps | 1 Kbps = 1,000 bps = $10^3$ bps |
| Megabits per second | Mbps | 1 Mbps = 1,000,000 bps = $10^6$ bps |
| Gigabits per second | Gbps | 1 Gbps = 1,000,000,000 bps = $10^9$ bps |
| Terabits per second | Tbps | 1 Tbps = 1,000,000,000,000 bps = $10^12$ bps |


##### Physical Layer Terminology

###### Latency
Latency refers to the amount of time - including delays - for data to travel from one point to another.

###### Throughput
Throughput is the measure of the transfer of bits over a medium during a given timeframe.

###### Goodput
Goodput is the measure of **usable** data transferred within a given timeframe. It acts as a term for measured throughput minus the neccessary traffic overhead.

##### Wireless Technology

Wireless carries electromagnetic signals representing binary digits with the use of radio/microwave frequencies (as they provide the most mobility). It has some limitations, however:

- Effective coverage can be impacted by surrounding physical characteristics of the location
- Susceptible to interference and disrupted by many common devices
- No physical access required (unlike wired), so anyone in range can access the transmission
- WLANs operate in half-duplex, meaning that when many users access the WLAN simultaneously, bandwidth drops for each user.

IEEE and telecom industry standards for wireless data communications define requirements for both Data Link and Physical layers of the OSI model. Dictated properties include:
- Data to radio signal-encoding methods
- Frequency and power of transmission
- Signal reception and decoding requirements
- Design and construction of antenna

Wireless standards include:

- Wi-Fi (IEEE 802.11) - defines WLAN technology
- Bluetooth (IEEE 802.15) - Wireless Personal Area Network (WPAN) standard
- WiMAX (IEEE 802.16) - Uses a point-to-multipoint topology to provide broadband wireless access
- Zigbee (IEEE 802.15.4) Low datarate, power-consumption comms standard intended for Internet of Things (IoT) applications.

Wireless LANs (WLANs) require the following devices:
- A Wireless Access Point (WAP)
	- Concentrates wireless signals from users and connects to existing copper-based networking infrastructure
- Wireless NICs
	- Provides wireless networking capabilities to hosts

There are many WLAN standards, so compatibility and interoperability must be ensured when purchasing equipment. Due to the aforementioned limitations, netadmins must apply stringent policy and process to secure WLANs from unauthorized access and damage.


### TCP/IP

| TCP/IP Model Layer | Description |
| ------------------ | ----------- |
| Application | Represents data to the user, plus encoding and dialog control. |
| Transport | Supports communication between various devices across diverse networks. |
| Internet | Determines the best path through the network. |
| Network Access | Controls the hardware devices and media that make up the network. |

### Comparison of OSI & TCP/IP

![[CompareOSI_TCPIP.png]]

The OSI model divides the network and application layer of the TCP/IP model into multiple layers, and layers 1 and 2 discuss the neccessary procedures to access media and the physical means to send data over a network. This is in contrast to TCP/IP, which does not specify which protocols should be used when transmitting over a physical medium.

### IPv4 Protocol Diagram

![[IPv4ProtoDiag.png]]

#### Diagram Fragmentation

Network links have a Maximum Transfer Unit (MTU) which refers to the largest possible link-level frame. Different link types have dfiferent MTUs. Large IP datagrams are fragmented within the network itself; one datagram becomes several that are reasseembled at the final destination, with IP header bits used to identify and order the individual fragments themselves.

![[DiagFrag.png]]

#### Protocol Addressing

Interfaces are connected via wired Ethernet interfaces connected by Ethernet switches, and wireless WiFi interfaces connection via a WiFi base station.

#### Protocol Subnetting

An IP address consists of two parts; the *subnet part* - which contains high order bits, and the *host part,* which contains low order bits. Subnets themselves are device interfaces with the same subnet part of their IP address. They can physically reach eachother without an intervening router.

To determine subnets each interface is detached from its host or router in order to create islands of isolated networks. Each of these is called a *subnet.*

##### Subnetting example

A large enterprise requires at least 100 subnets, choosing the private address 172.16.0.0/16 as an internal network address.

The below image displays the number of creatable subnets when borrowing bits from the third and fourth octets. There are now up to 14 host bits that can be borrowed; the last two bits cannot be borrowed as they have already been reserved for devices.

![[SubnetEx1.png]]

Therefore in order to satisfy requirements, 7 bits:  ($2^7 = 128$ subnets) need to be borrowed, for a total of 128 subnets. The table below highlights all possible scenarios for subnetting a /16 prefix IP:

![[SubnetEx2.png]]

### Half and Full Duplex Communication

#### Half-Duplex

Half-duplex communication only allows one device to send or receive at a time over a single shared medium. It is commonly used on WLANs and legacy bus topologies that contain Ethernet hubs.

#### Full-Duplex

Full-duplex communication allows both devices to simultaneously transmit and recieve over a shared medium. Ethernet switches operate in full-duplex.