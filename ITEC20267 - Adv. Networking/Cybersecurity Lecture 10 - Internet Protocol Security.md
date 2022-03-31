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

In order to decide what protection is to be provided for an outgoing packet, IPsec can uniquely identify an SA by their *Security Parameters Index* (SPI), a destination IP, and a security protocol identifier (from AH or ESP). It should be noted that the SPI is stored within the header of both AH and ESP packets.

A similar procedure is used for incoming packets. It should be noted that the actual choice of encryption and authentication algorithm is left to the administrator of an IPsec-aware network.

### Internet Key Exchange Protocol

SAs can be created manually if the number of nodes is small, but this obviously does not scale to reasonable sized networks of IPsec-aware hosts.

The *Internet Key Exchange* (IKE) protocol is used to automatically set up SAs by handling the negotiation of protocols/algorithms, and generation of encryption/authentication keys to be used by IPsec.

The security goals of IKE are as follows:
- Entity authentication
- Establishing fresh shared secrets
- Secure negotiation of all cryptographic algorithms

### IPsec Example

See <a href = "https://ntu.cloud.panopto.eu/Panopto/Pages/Viewer.aspx?id=341f64b7-02b7-4fcd-a748-adf100a83bb1&start=2546.578999">this point in the lecture</a> for a video description.

![[Pasted image 20211201173939.png]]

### Takeaway Remarks on IPsec

IPSec provides *transparent* security for all users of the IP protocol, without fundamentally changing the interface of IP itself. It provides host-to-host security but *not* user-to-user or application-to-application security.

As a result, IPsec protects and application traffic *across an IP network* - applications themselves do not need to be specifically designed to use IPsec.

The main application of IPsec is in the use of *Virtual Private Networks* (VPNs).

