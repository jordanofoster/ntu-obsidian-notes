`NOTE: This is being covered because Advanced Networking Coursework has a component on IPv6 security that has not been taught about within the module`

# Internet Protocol Security

## TCP/IP Protocol Suite

![[Pasted image 20211201171836.png]]

### Internet Protocol

The Internet Protocol (IP) is the principal communications protocol used to relay datagrams (packets) across an internet. It works using the Internet Protocol Suite.

IP is a connectionless and stateless protocol; a datagram is a basic transfer unit associated with a packet-switched network, and each datagram is treated as an independent entity. The delivery, arrival time and order of datagrams are not guaranteed.


#### Internet Protocol Security

IPsec is a protocol suite for securing IP communications by authenticating and encrypting each packet of a data stream. It works as an end-to-end security scheme, operating in the *Internet Layer* of the IP suite. IPsec uses the following:

- Authentication header
- Encapsulating security payloads
- Security associations
- Internet key exchange

IPsec is optional for IPv4; but mandatory for IPv6.

##### Authentication Header

The Authentication Header (AH) protects connectionless integrity and provides data origin authentication of packets. AHs can also protect against replay attacks by discarding old packets, but they *do not* protect confidentiality.

![[Pasted image 20211201172422.png]]

##### Encapsulating Security Payload

The Encapsulating Security Payload (ESP) can be used to provide confidentiality, data origin authentication, data integrity, and *some* replay protection.

![[Pasted image 20211201172501.png]]

###### ESP Fields 

- Security Parameters Index (32 bits)
	- Used together with source IP address to identify the *security association* of the sending party.
- Sequence Number (32 bits)
	- A monotonically increasing sequence number to protect against replay attacks.
-  