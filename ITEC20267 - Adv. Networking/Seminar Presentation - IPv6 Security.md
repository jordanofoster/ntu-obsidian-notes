# IPv6 Security
## Overview of IPv6
IPv6 has recently become mandatory as the IANA has declared IPv4 deprecated. Compared to IPv4, IPv6 also supports many new features, including:
- An increased address space
	- New packet structure with 128-bit long source/destination IP addresses - *four times larger* than IPv4, meaning *more possible addresses.*
- Autoconfiguration
- Quality-of-Service capabilities
- Network-layer security.

## IPv6 Packet Format
### IPv6 Datagram Packets (UDP)
The base header occupies 40 bytes, whereas the payload can contain up to 65,535 bytes of information, as  seen below:

![[Pasted image 20220331215309.png]]

The components of an IPv6 Datagram Packet are explained as follows:
- Version (4-bit) - defines the version number of the IP protocol being used. For IPv6, this is `6`.
- Traffic class (8-bit) - this distinguishes between different payloads, with different delivery requirements; and replaces the *type-of-service* field in IPv4.
- Flow label (20-bit) - Designed to provide special handling for a particular flow of data. 
	- This allows us to use IPv6 as a *connection-oriented* protocol.
	- In its simplest form, flow labels can be used to have a router process the packet quicker.
- Payload length (16-bit/2 bytes) - This defines the length of the IP datagram packet (excluding the header component).
- Next header (8-bit) - Defines the type of the first *extension* header.
- Hop limit (8-bit) - Serves the same purpose as the *Time-to-Live* field in IPv4 packets.
- Source/Destination Address (128-bits/16 bytes each) - defines source and destination IP addresses.

Finally, the *Payload* field in IPv6 has a different format and meaning than the *Payload* field in IPv4.

#### Payloads in an IPv6 Datagram
The payload in IPv6 contains a combination of one or more *extension* headers, or options, followed by the headers/payloads of the protocol in the *layer above it* - such as TCP, UDP, etc.

![[Pasted image 20220331215952.png]]

Each extension's header has *two mandatory fields;* the *next* header, and the extension length. The *code* of the *next header* field (its value) defines the *type* of the header after it, as seen in the diagram above.

The *last* "next header" field in the extension list *defines the protocol in the payload* (TCP/UDP/etc.)

### Extension Headers
The base header can be followed by up to *six* extension headers, as seen below:
![[Pasted image 20220331220232.png]]

We will describe the options from left-to-right:
- The *hop-by-hop* option is used when the source needs to pass information to *all routers* that the datagram packet visits.
- The *destination* option is used when the source needs to pass information to the *destination only.*  Intermediate routers are *not* permitted access to this information.
- For *fragmentation,* the concept is the same in IPv6 as in IPv4.
- The *authentication* extension header has two purposes:
	- It validates the message sender...
		- This is needed so that the receiver can be certain that the message is from a *genuine sender,* and *not* an imposter.
	- ...and ensures integrity of data.
		- This checks that the data has not been altered during transmission, either accidentally or maliciously (i.e. by an adversary).
- The *Encrypted Security Payload* (ESP) provides confidentiality and protects against eavesdropping.

## IP Security (IPSec) overview:
[[Cybersecurity Lecture 10 - Internet Protocol Security|Make sure to see the related Cyber-Security lecture on the same topic.]]

In IPv6, IPSec is part of the protocol suite, and is *mandatory.* IPSec itself is a set of security specifications, originally written as part of the IPv6 specification itself. A diagram describing the three main features of the specification is shown below:

![[Pasted image 20220331221343.png]]

### Where can we implement IPSec?
There are two main areas where IPSec can be implemented:
- at the *End Host*
	- This provides the most flexibility and security...
	- ...but is far more work if there are many hosts.
- at the *Router*
	- We only have to make limited changes to a *few routers*
		- and provide connections between these routers.

### Applications of IPSec
IPSec provides the capability to secure communications across LANs, private *and* public WANs, and across the Internet. Examples of its use include:

- **Secure branch connectivity over the Internet:**
	- Companies can build a secure VPN over the Internet, or a public WAN.
- **Secure remote access over the Internet:**
	- An end user whose system is equipped with IPsec protocols can make a local call to an ISP, and gain secure access to a company network.
- **Establishing extranet and intranet connectivity with partners:**
	- IPsec can be used for secure communications with other organisations.
		- This ensures authentication and confidentiality, an provides a key exchange mechanism.
- **Enhancing e-commerce security:**
	- Even though some web/e-commerce applications have built-in security protocols, IPsec enhances their security.

### Modes of IPsec
#### Transport Mode
This protects the *upper-layer* protocols:

![[Pasted image 20220331222342.png]]

#### Tunnel Mode
This protects the *entire IP payload*