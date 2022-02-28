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

