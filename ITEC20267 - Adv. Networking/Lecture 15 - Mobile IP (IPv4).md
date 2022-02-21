# Mobile IP (IPv4)

*Mobile IP* is a standard communication protocol, defined to allow mobile device users to move from one IP network to another, while maintaining a static IP address. Mobile networking is important, both in the present (vehicular networking) and future (moving hosptials with 5G)

Mobile networking should *not* be confused with portable networking; the latter requires a connection to the same ISP (unlike the former).

## Portable Networking

Portable networking includes the following systems/protocols:
- Cellular Systems
	- Cellular Digital Packet Data (CDPD)
	- 3G
- Bluetooth
	- Low-cost, short-range radio links between mobile devices
- Wireless Ethernet (802.11)
	- Widely used wireless MAC layer technology.

## Standard IP routing

IP by default assumes that end hosts are in fixed physical locations, and does not accomodate for if a host moves *between* networks. IP addresses themselves enable IP routing algorithms to get packets to the current network:
- Each IP address has a network and host component, keeping host specific information outside of routers.
- DHCP is used to get packets to end hosts in networks; this still assumes a *fixed* end host, however.

What do we do if users want to roam between networks?
- Mobile users do not want to know that they are moving between networks (distracting!)
- Why can't mobile users change their IP when running an application?

## Mobile IP - The Standard

Mobile IP was developed as a means for transparently dealing with the problems of mobile users. It provides the following functionality:
- Enables hosts to stay connected to the Internet, regardless of location
- Enables hosts to be tracked, without changing their IP address
- Requires no changes to the software of non-mobile hosts/routers
- Requires *some* additions to existing infrastructure
- No geogrp
