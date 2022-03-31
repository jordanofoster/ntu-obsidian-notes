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
The payload in IPv6 contains a combination of one or more *exn*