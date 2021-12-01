`NOTE: This is being covered because Advanced Networking Coursework has a component on IPv6 security that has not been taught about within the module`

# Internet Protocol Security

## TCP/IP Protocol Suite

![[Pasted image 20211201171836.png]]

## Internet Protocol

The Internet Protocol (IP) is the principal communications protocol used to relay datagrams (packets) across an internet. It works using the Internet Protocol Suite.

IP is a connectionless and stateless protocol; a datagram is a basic transfer unit associated with a packet-switched network, and each datagram is treated as an independent entity. The delivery, arrival time and order of datagrams are not guaranteed.


### Internet Protocol Security

IPsec is a protocol suite for securing IP communications by authenticating and encrypting each packet of a data stream. It works as an end-to-end security scheme, operating in the *Internet Layer* of the IP suite. IPsec uses the following:

- Authentication header
- Encapsulating security payloads
- Security associations
- Internet key exchange

IPsec is optional for IPv4; but mandatory for IPv6.

#### Authentication Header

The Authentication Header (AH) protects connectionless integrity and provides data origin authentication of packets. AHs can also protect against replay attacks by discarding old packets, but they *do not* protect confidentiality.

![[Pasted image 20211201172422.png]]

#### Encapsulating Security Payload

The Encapsulating Security Payload (ESP) can be used to provide confidentiality, data origin authentication, data integrity, and *some* replay protection.

![[Pasted image 20211201172501.png]]

##### ESP Fields 

- Security Parameters Index (32 bits)
	- used together with source IP address to identify the *security association* of the sending party.
- Sequence Number (32 bits)
	- A monotonically increasing sequence number to protect against replay attacks.
- Payload data (variable)
	- The protected contents of the original IP packet.
- Padding (0-255 octets)
	- Padding for encryption, to extend the payload data to a size that fits the encryption's cipher block size, and to align the next field
- Authentication data (variable, multiple of 32 bits)
	- Integrity check value

##### ESP Modes

There are two modes of ESP; *Transport* and *Tunnel* mode.

###### Transport Mode

![[Pasted image 20211201172908.png]]

In *Transport Mode*, an upper-layer protocol frame (e.g. from TCP or UDP) is encapsulated within the ESP. The header IP is *not* encrypted.

Transport mode provides end-to-end protection of packets exchanged between two end hosts; both nodes have to be IPsec aware, however.

###### Tunnel Mode

![[Pasted image 20211201172930.png]]

In *Tunnel Mode*, both the entire datagram *and* the ESP fields are treated as a new payload of an outer IP datagram packet. The original (inner) datagram packet is encapsulated within the outer packet. As a result, IP tunnelling tends to be described as *IP-within-IP*.

Tunnel mode has the advantage of *end* hosts not needing to be aware of IPsec's existence.

##### Security Associations

To generate, decrypt or verify an ESP packet, a system requires knowledge of which algorithm and key to use. A *Security Association* (SA) refers to the bundle of algorithms and parameters, such as keys, that is being used to encrypt and authenticate a particular data flow, in *one direction.*

In bidirectional traffic, flows are secured using a *pair* of SAs instead.

Security Associations may include the following:

- Cryptographic algorithm and mode
- Traffic encryption keys and their lifetimes
- Parameters for network data to be passed over the connection
- Protocol mode (Tunnel/Transport)
- (Possibly) initialisation vectors.

The list of active SAs is held in the *Security Association Database* (SAD).

In order to decide what protection is to be provided for an outgoing packet, IPsec can uniquely identify an SA by their *Security Parameters Index* (SPI).

SPI is carried in both AH and E