# TCP
## Transport Layer
The transport layer provides *logical communication* between application-layer processes running on different hosts. Transportation protocols themselves run on end systems as two sides:

- On the sending side, the protocol breaks application messages into *segments* and passes them onto the network layer.
- On the receiving side, segments are reassembled into messages and passed back to the application layer.

More than one transportation layer protocol is available to applications, with the main two being TCP and UDP.

## UDP
UDP is a very barebones Internet transport protocol that attempts to be a best effort service; UDP segments may be lost or delivered out-of-order to the application. The protocol is *connectionless*, meaning that no handshaking occurs between the sender and receiver, and each UDP segment is treated independently of others (i.e. there is no packet numbering).

UDP is typically used for applications where bandwidth is limited, be it by the amount of data transferred or the lack of quality in the connection itself. This includes things such as streaming/multimedia apps (which can compensate for packet loss - but not for low data rates), and network-discovery protocols such as DNS and SNMP. The protocol itself lacks any reliability measures, and as such they must be implemented at the application layer (such as error recovery).

### UDP Segment Format
![[Pasted image 20220111215300.png]]
In this instance, `length` refers to the length of the UDP segment as a whole in bytes (including the header).

#### Why does UDP exist?
Several aspects of UDP's sister protocol, TCP, add delay to network communications, including:
	- Connection establishment
	- Tracking connection state
	
UDP naturally does not face these issues. In addition, the protocol's small header size reduces overhead further, and the lack of congestion control means that UDP's only limits on data-rate are those imposed by the layers below it. This makes it naturally suitable for situations where data needs to reach another system q