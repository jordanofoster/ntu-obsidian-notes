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
- No geographical limitations are present
- No modifications to IP addresses (or the format itself) is required.
- Mobile IP itself also supports security.

Mobile IP itself could be even more important than physically connected routing; the IETF standardiziation process is still underway[^citation needed].

### Mobile IP Entities 

#### Mobile Node (MN)

This is an entity that can change its point of attachment from network-to-network, within the internet. MNs detect that they have moved and register themselves with the 'best' FA. Mobile nodes are assigned a permanent IP (called its *home* address), to which other hosts send packets - regardless of that MN's location.

Since an MN's home IP doesn't change, it can be used by long-lived applications - even as the MN's location changes.

#### Home Agent (HA)

This is effectively a router with additional functionality, located on the home network of the MN. It does mobility binding of the MN's IP with the MN's Care-of-address (COA), and forwards packets to an appropriate network when the MN is away through encapsulation.

#### Foreign Agent (FA)

Foreign agents are another agent (*not* the HA) with enhanced functionality. If the MN is away from the HA, it uses a FA to send/recieve data to/from its HA. Foreign agents advertise themselves periodically over the network, and forward the registration requests of MNs and decapsulate messages for delivery to them.

#### Care-of-address (COA)

This is an address that identifies the MN's current location, and is sent by the FA to the HA when the MN attaches to it. The COA is typically the IP address of the FA itself.

#### Correspondent Node (CN)

CNs are the end host to which the MN corresponds (such as a web server).





