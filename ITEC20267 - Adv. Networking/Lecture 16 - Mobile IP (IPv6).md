# Mobile IP (IPv6)
## Modes of communication
There are two modes of communication between a mobile node and correspondent node in Mobile IPv6:
- Bidirectional tunneling
	- This does not require the correspondent to support Mobile IPv6
- Route Optimization
	- This requires the mobile node to register its current IP binding at the correspondent.
	- Packets from the correspondent can be routed direct to the COA of the mobile node.

## Mobile IP Extension Headers
[[MobileIPv6ExtensionHeaders.m4a|Commentary.]]
![[Pasted image 20220228130856.png]]

## Mobile IP Source Routed Packet
[[MobileIPSourceRoutedPacket.m4a]]
![[Pasted image 20220228131504.png]]

## Mobile IP Routing in IPv6
[[MobileIPRoutingInIPv6.m4a]]
![[Pasted image 20220228131650.png]]

## Mobile IP Reverse Tunnelling
[[MobileIPReverseTunnelling.m4a]]
![[Pasted image 20220228131818.png]]#

## Mobile IP Agenda
[[MobileIPAgenda.m4a]]
![[Pasted image 20220228131855.png]]

## Mobile IP Security
Binding updates make use of IPSec extension headers, or alternatively via th *Binding Authorisation Data* option. Prefix discovery is protected using the IPSec headers and mechanisms related to transporting payload packets (such as the *Home Address Destination* option and type 2 routing header) have been designed such that their use in attacks is restricted.

## NEMO

[[NEMO.m4a|NEMO refers to (NE)tworks in (MO)tion]] - a working group established in the IETF during December 2002, concerned with managing mobility across entire networks - which change their point of attachment to the internet (and thus reachability in the topology) as a unit.

### Goals of NEMO

NEMO intends to standardize some basic support mechanisms based on bidirectional tunnelling  (completed January 2005) and to study the possible approaches and issues with providing more optimal routing.

### NEMO Protocol

Solutions must meet the following criterium: 
- Must use bidirectional tunnels
- MNNs must be reachable at a permanent IP with associated name.
- Continuous sessions (both unicast and multicast) between MMNs and arbitrary CNs must be maintained after IP handover to one of the MRs.
- Must not require modifications to nodes other the MRs and HAs.
- Must support fixed nodes, mobile hosts and mobil routers in the mobile network.
- Must not prevent the proper operation of Mobile IPv6:
	- i.e. Must support MIPv6-enabled MNNs and must allow MNNs to receive and process binding updates from arbitrary mobile nodes.
- Must treat all potential configurations the same, regardless of number of subnets, MMNs, nested levels of MRs, egress interfaces, etc.
- Must support mobile networks attaching to other mobile networks (known as nested mobile networks).

[[NEMOFeatures.m4a|NEMO is also responsible for providing the following:]]

- Route optimization
- Load sharing (monami)
- Policy Based Routing (monami)
- Multiple Home Agents from different Service Providers
	- These have security issues
	- Desirable for some applications (i.e. air traffic control, airline maintenance, entertainment)

## Benefits of IPv6 in MANETs

- IPv6 coupled together with MANET offers ease and speed of deployment, with reduced infrastructure reliance.
- End-to-End Global Addressing
- Autoconfiguration of link-local addresses
- End-to-End security (possibly) via IPSec integration
- Support for source routing
- Full mobility support
- No broadcast traffic to hamper wireless network efficiency
- Potential support of real-time data delivery via QoS
- Potential to utilize Anycast addressing

### Challenges of Mobile IP in MANETs
[[MobileIPMANETChallenges.m4a]]
[[MobileIPMANETChallenges2.m4a]]
- Denial of Service
	- DAD DoS, Uncooperative routers, etc.
	- Neighbor discovery trust and threats
- Network discovery
	- Reachback, DNS, Key Manager
- Security
	- IPSec/HAIPES tunnel end-points
	- Security Policies in a dynamic environment
	- Is layer-2 encryption sufficient?
	- Insecure routing
		- Attackers can inject erroneous routing info to divert traffic or make routing inefficient
- Key Management
	- Lack of key distribution mechanism
	- Hard to guarantee access to any particular node by obtaining a secret key
- Duplicate Address Discovery
	- Not suitable for multihop adhoc networks that have dynamic topologies
	- Situation where two MANET partitions merge needs addressing
- Radio Technology
	- Layer-2 media access often incompatible with layer-3 MANET routing protocol
- Battery exhaustion threat
	- A malicious node may interact with a mobile node very often, trying to drain the latter's battery.
- Testing of Applications
- Integrating MANET into the Internet

