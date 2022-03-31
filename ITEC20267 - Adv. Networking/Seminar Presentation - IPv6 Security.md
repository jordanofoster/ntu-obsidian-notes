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
- Version (4-bit) - defines the version number of the IP protocol being used. For IPv6, this is `6`