# Using IPv6 Addressing

## The Need for IPv6

IPv4 is running out of addresses; IPv6 acts as a successor to it, having a much larger 128-bit address space. The development of IPv6 also includes fixes for IPv4 limitations alongside other enhancements. 

With an increasing internet population, a limited IPv4 address space, issues with NAT and the IoT, the time has come where transitioning to IPv6 must begin.

## Coexistence between IPv4 and IPv6

Both IPv4 and IPv6 will coexist in the near future, as the transition to IPv6 will take several years; the IETF has created various protocols and tools to help network administrators migrate their networks to IPv6. These migration techniques can be divided into three categories:

- **Dual stack** - The devices run both IPv4 and IPv6 protocol stacks simultaneously
- **Tunneling** - A method of transporting an IPv6 packet over an IPv4 network. The IPv6 packet is encapsulated inside an IPv4 packet.
- **Translation** Network Address Translation 64 (NAT64) allows IPv6-enabled devices to communicate with IPv4-enabled devices using a translation technique similar to NAT for IPv4.

## IPv4 Addressing Formats

IPv6 addresses are 128 bits in length, written in hexadecimal. They are not case-sensitive and can be written in either lower or uppercase. The preferred format for writing an IPv6 address is `x:x:x:x:x:x:x:x`, with each `x` consisting of four hexadecimal values. In IPv6, a hextet is the unofficial term used to refer to a segment of 16 bits, or 4 hexadecimal values. Examples of IPv6 addresses in the preferred format are below:

`2001:0db8:0000:1111:0000:0000:0000:0200`
`2001:0db8:0000:00a3:abcd:0000:0000:1234`

### Rule 1 - Omit Leading Zero

The first rule to help reduce the notation of IPv6 addresses is to omit any leading 0s. For example:

- `01ab` can be represented as `1ab`
- `09f0` can be represented as `9f0`
- `0a00` can be represented as `a00`
- `00ab` can be represented as `ab`

Note: this rule only applies to leading 0s: if it was applied to trailing 0s, the address would be ambiguous.

| Type | Format |
| ---- | ------ |
| Preferred | 2001 : **0**db8 : **000**0 : 1111 : **000**0 : **000**0 : **000**0: **0**200 |
| No leading zeros | 2001 : db8 : 0 : 1111 : 0 : 0 : 0 : 200 |

### Rule 2 - Double Colon

A double colon (`::`) can replace any single, contiguous string of one or more 16-bit hextets consisting of all zeros. For example:

`2001:db8:cafe:1:0:0:0:1` (leading 0s omitted) could be represented as `2001:db8:cafe:1::1`

Note: the double colon (`::`) can only be used once within an address; otherwise there would be more than one possible resultant.

| Type | Format |
| ---- | ------ |
| Preferred | 2001 : **0**db8 : **000**0 : 1111 : **0000** : **0000** : **0000** : **0**200 |
| Compressed | 2001:db8:0:1111::200

## IPv6 Address Types

There are three broad categories of IPv6 addresses:

- **Unicast** - uniquely identifies an interface on an IPv6-enabled device
- **Multicast** - used to send a single IPv6 packet to multiple destinations.
- **Anycast** - This is any IPv6 unicast address that can be assigned to multiple devices. A packet sent to an anycast address is routed to the nearest device having that address.

Note: Unlike IPv4, IPv6 does not use broadcast addresses. However, IPv6 all-nodes multicast addresses exist that essentially give the same result.

### IPv6 Prefix Length

Prefix length is noted in slash notation, used to indicate the network portion of an IPv6 address. The length can range from 0 to 128; the recommended IPv6 prefix length for LANs and most other types of networks is `/64`.

![[IPv6PrefixLenDiag.png]]

Note: It is strongly recommended to use a 64-bit Interface ID for most networks. This is because stateless address autoconfiguration (SLAAC) uses 64 bits for the Interface ID. It also makes subnetting easier to create and manage.

### Types of IPv6 Unicast Addresses

![[IPv6UnicastTypes.png]]

Unlike IPv4 devices that have only a single address, IPv6 addresses typically have two unicast addresses:

- **Global Unicast Address (GUA)** – This is similar to a public IPv4 address. These are globally unique, internet-routable addresses.
- **Link-local Address (LLA)** - Required for every IPv6-enabled device and used to communicate with other devices on the same local link. LLAs are not routable and are confined to a single link.

#### IPv6 GUAs

IPv6 global unicast addresses (GUAs) are globally unique and routable on the IPv6 internet; currently, only GUAs with the first three bits of 001 or 2000::/3 are being assigned. Currently available GUAs begin with a decimal 2 or a 3. This is only 1/8th of the total available IPv6 address space.

![[IPv6GUAs.png]]

##### Structure of IPv6 GUAs

Note: IPv6 allows the all-0s and all-1s host addresses can be assigned to a device. The all-0s address is reserved as a Subnet-Router anycast address, and should be assigned only to routers.

###### Global Routing Prefix

The global routing prefix is the prefix, or network, portion of the address that is assigned by the provider, such as an ISP, to a customer or site. The global routing prefix will vary depending on ISP policies.

###### Subnet ID

The Subnet ID field is the area between the Global Routing Prefix and the Interface ID. The Subnet ID is used by an organization to identify subnets within its site.

###### Interface ID

The IPv6 interface ID is equivalent to the host portion of an IPv4 address. It is strongly recommended that in most cases /64 subnets should be used, which creates a 64-bit interface ID.

#### IPv6 LLAs

An IPv6 link-local address (LLA) enables a device to communicate with other IPv6-enabled devices on the same link and only on that link (subnet). Packets with a source or destination LLA cannot be routed.

Every IPv6-enabled network interface must have an LLA. If an LLA is not configured manually on an interface, the device will automatically create one. IPv6 LLAs are in the fe80::/10 range.

![[IPv6LLAs.png]]

### Unique Local Addresses

The IPv6 unique local addresses (range fc00::/7 to fdff::/7) have some similarity to RFC 1918 private addresses for IPv4, but there are significant differences:

- Unique local addresses are used for local addressing within a site or between a limited number of sites.
- Unique local addresses can be used for devices that will never need to access another network.
- Unique local addresses are not globally routed or translated to a global IPv6 address.

Note: Many sites use the private nature of RFC 1918 addresses to attempt to secure or hide their network from potential security risks. This was never the intended use of ULAs.

### Static GUA Configuration on a Router

Most IPv6 configuration and verification commands in the Cisco IOS are similar to their IPv4 counterparts. In many cases, the only difference is the use of `ipv6` in place of `ip` within the commands. The command to configure an IPv6 GUA on an interface is: `ipv6 address <ipv6-address/prefix-length>`.

The example below shows commands to configure a GUA on the G0/0/0 interface on R1:

![[CLIConfigStaticGUA.png]]

### Static GUA Configuration on a Windows Host

![[WinGUIStaticGUAConfig.png]]

Manually configuring the IPv6 address on a host is similar to configuring an IPv4 address. The GUA or LLA of the router interface can be used as the default gateway. Best practice is to use the LLA.

Note: When DHCPv6 or SLAAC is used, the LLA of the router will automatically be specified as the default gateway address.

### Static GUA Configuration of a Link-Local Unicast Address

Configuring the LLA manually lets you create an address that is recognizable and easier to remember. LLAs can be configured manually using the `ipv6 address <ipv6-link-local-address> link-local` command. 

The example below shows commands to configure a LLA on the G0/0/0 interface on R1:

![[CLIStaticGUALinkLocalUnicastAddrConfig.png]]

Note: The same LLA can be configured on each link as long as it is unique on that link. Common practice is to create a different LLA on each interface of the router to make it easy to identify the router and the specific interface.

### Dynamic Addressing for IPv6 GUAs: RS and RA Messages

Devices obtain GUA addresses dynamically through Internet Control Message Protocol version 6 (ICMPv6) messages. 

- **Router Solicitation (RS)** messages are sent by host devices to discover IPv6 routers. 
- **Router Advertisement (RA)** messages are sent by routers to inform hosts on how to obtain an IPv6 GUA and provide useful network information such as:
	- Network prefix and prefix length
	- Default gateway address
	- DNS addresses and domain name
- The RA can provide three methods for configuring an IPv6 GUA :
	- SLAAC
	- SLAAC with stateless DHCPv6 server
	- Stateful DHCPv6 (no SLAAC)

####  Method 1: Stateless Address Auto-configuration - SLAAC

SLAAC allows a device to configure a GUA without the services of DHCPv6. Devices obtain the necessary information to configure a GUA from the ICMPv6 RA messages of the local router. The prefix is provided by the RA and the device uses either the EUI-64 or random generation method to create an interface ID.

![[SLAACDiag.png]]

#### Method 2: SLAAC and Stateless DHCP

An RA can instruct a device to use both SLAAC and stateless DHCPv6. The RA message suggests devices use the following:

- SLAAC to create its own IPv6 GUA
- The router LLA, which is the RA source IPv6 address, as the default gateway address
- A stateless DHCPv6 server to obtain other information such as a DNS server address and a domain name

![[SLAACStatelessDHCP.png]]

#### Method 3: Stateful DHCPv6

An RA can instruct a device to use stateful DHCPv6 only. Stateful DHCPv6 is similar to DHCP for IPv4. A device can automatically receive a GUA, prefix length, and the addresses of DNS servers from a stateful DHCPv6 server. The RA message suggests devices use the following:

- The router LLA, which is the RA source IPv6 address, for the default gateway address.
- A stateful DHCPv6 server to obtain a GUA, DNS server address, domain name and other necessary information.

### Extended Unique Identifier - EUI-64 Process vs. Randomly Generated

When the RA message is either SLAAC or SLAAC with stateless DHCPv6, the client must generate its own interface ID. The interface ID can be created using the EUI-64 process or a randomly generated 64-bit number.

![[EUI64vsRandomGen.png]]

#### EUI-64 Process

The IEEE defined the Extended Unique Identifier (EUI) or modified EUI-64 process which performs the following:

- A 16 bit value of `fffe` (in hexadecimal) is inserted into the middle of the 48-bit Ethernet MAC address of the client.
- The 7th bit of the client MAC address is reversed from binary `0` to `1`.

As an example:

| 48-bit MAC | `fc:99:47:75:ce:e0` |
| ---------- | ----------------- |
| EUI-64 Interface ID | `fe:99:47:ff:fe:75:ce:e0` 


#### Randomly Generated Interface IDs
   
Depending upon the operating system, a device may use a randomly generated interface ID instead of using the MAC address and the EUI-64 process. Beginning with Windows Vista, Windows uses a randomly generated interface ID instead of one created with EUI-64.

![[WinRandInterfaceIDExample.png]]

Note: To ensure the uniqueness of any IPv6 unicast address, the client may use a process known as Duplicate Address Detection (DAD). This is similar to an ARP request for its own address. If there is no reply, then the address is unique.

### Dynamic Addressing for IPv6 LLAs

All IPv6 interfaces must have an IPv6 LLA. Like IPv6 GUAs, LLAs can be configured dynamically. The figure below shows that the LLA is dynamically created using the fe80::/10 prefix and the interface ID using the EUI-64 process, or a randomly generated 64-bit number.

![[DynAddrLLAsDiag.png]]

#### Dynamic LLAs on Windows

Operating systems, such as Windows, will typically use the same method for both a SLAAC-created GUA and a dynamically assigned LLA.

###### EUI-64 Generated Interface ID

![[WinEUI-64GenInterfaceID.png]]

###### Random 64-bit Generated Interface ID:

![[WinRand64-BitInterfaceID.png]]

### Assigned IPv6 Multicast Addresses
   
IPv6 multicast addresses have the prefix `ff00::/8`. There are two types of IPv6 multicast addresses: Well-Known multicast addresses, and Solicited node multicast addresses.

Note: Multicast addresses can only be destination addresses and not source addresses.

#### Well-Known IPv6 Multicast Addresses

Well-known IPv6 multicast addresses are assigned and are reserved for predefined groups of devices. There are two common IPv6 Assigned multicast groups:

- `ff02::1` **All-nodes multicast group** - This is a multicast group that all IPv6-enabled devices join. A packet sent to this group is received and processed by all IPv6 interfaces on the link or network.

- `ff02::2` **All-routers multicast group** - This is a multicast group that all IPv6 routers join. A router becomes a member of this group when it is enabled as an IPv6 router with the ipv6 unicast-routing global configuration command.

#### Solicited-Node IPv6 Multicast

A solicited-node multicast address is similar to the all-nodes multicast address and is mapped to a special Ethernet multicast address. The Ethernet NIC can filter the frame by examining the destination MAC address without sending it to the IPv6 process to see if the device is the intended target of the IPv6 packet.

![[SolNodeIPv6MultiDiag.png]]

### Subnetting an IPv6 Network using the Subnet ID

IPv6 was designed with subnetting in mind. A separate subnet ID field in the IPv6 GUA is used to create subnets; the subnet ID field is the area between the Global Routing Prefix and the interface ID.

![[SubnettingIDDiag.png]]

#### IPv6 Subnetting Example

![[IPv6SubnetExample.png]]

- Given the 2001:db8:acad::/48 global routing prefix with a 16 bit subnet ID.
- Allows 65,536 /64 subnets
- The global routing prefix is the same for all subnets.
- Only the subnet ID hextet is incremented in hexadecimal for each subnet.

#### IPv6 Subnet Allocation
   
The example topology requires five subnets, one for each LAN as well as for the serial link between R1 and R2. The five IPv6 subnets were allocated, with the subnet ID field 0001 through 0005. Each /64 subnet will provide more addresses than will ever be needed.

![[IPv6SubnetAllocDiag.png]]