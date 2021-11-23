# Virtual Local Area Networks (VLAN)

`This lecture replicates Cisco online teaching materials.`

## Definition of a VLAN

![[Pasted image 20211122230822.png]]

VLANs are logical connections with other similar devices; placing devices into various VLANs have the following characteristics:
- Provides segmentation of the various groups of devices on the same switches
- Provides organizations with more manageable networks:
	- Broadcasts, multicasts and unicasts are isolated within the individual VLAN
	- Each VLAN has its own unique range of IP addressing
	- Smaller broadcast domains

### Benefits of a VLAN

![[Pasted image 20211122233642.png]]

| Benefits | Description |
| -------- | ----------- |
| Smaller Broadcast Domains | Dividing the LAN reduces the number of broadcast domains |
| Improved Security | Only users in the same VLAN can communicate together |
| Improved IT Efficiency | VLANs can group devices with similar requirements, e.g. faculty vs. students |
| Reduced Cost | One switch can support multiple groups/VLANs |
| Better Performance | Small broadcast domains reduce traffic, improving bandwidth |
| Simpler Management | Similar groups will need similar applications and other network resources |

### Types of VLAN 

#### Default VLAN

![[Pasted image 20211122233900.png]]

VLAN 1 is the following:
 - Default VLAN
 - Default Native VLAN
 - Default Management VLAN
 - Cannot be deleted or renamed

It should be noted that while VLAN1 cannot be deleted, Cisco recommends assigning these default features to other VLANs.

#### Data VLAN

These are dedicated to user-generated traffic, such as email and web traffic. VLAN1 is the default Data VLAN because all interfaces are assigned to it.

#### Native VLAN

This is used for trunk links only. All frames are tagged on an 802.1Q trunk link, except for those on the native VLAN.

#### Management VLAN

This is used for  SSH/Telnet VTY traffic, and should not be carried with end-user traffic. Management VLANs are also those that are the SVI for the Layer 2 switch.

#### Voice VLAN

![[Pasted image 20211122234317.png]]

A separate VLAN is required for voice traffic because it requires the following:
- Assured bandwidth
- High QoS priority
- Ability to avoid congestion
- Delay < 150ms from source -> destination

The entire VLAN network must be designed to serve this purpose.

### VLANs in a Multi-Switched Environment

#### Defining LAN Trunks

![[Pasted image 20211122234501.png]]

Trunks are point-to-point links between two network devices. Cisco trunk functions do the following:
- Allow more than one VLAN
- Extend the VLAN across the entire network
- Supports all VLANs by default
- Supports 802.1Q trunking

#### Networks without VLAN

![[Pasted image 20211122234630.png]]

Without VLANs, all devices connected to the switches receive all unicast, multicast and broadcast traffic.

#### Networks with VLANs

![[Pasted image 20211122235117.png]]

With VLANs, unicast, multicast and broadcast traffic if confined to a VLAN. Without a Layer 3 device to connect each VLAN, devices in different networks cannot communicate.

#### VLAN Identification with a Tag

![[Pasted image 20211122235133.png]]

The IEE 802.1Q header is 4 bytes long. When the tag is created, the FCS must be recalculated. When sent to end devices, this tag must be removed and the FCS recalculated back to its original number.

| 802.1Q VLAN Tag Field | Function |
| --------------------- | -------- |
| Type | 2-Byte field with hexadecimal `0x8100`. This is referred to as the Tag Protocool ID (TPID). |
| User Priority | 3-bit value that supports `note: blank here? fill later` |
| Canonical Format Identifier (CFI) | 1-bit value that can support token ring frames on Ethernet |
| VLAN ID (VID) | 12-bit VLAN identifier that can support up to 4096 VLANs |

##### Native VLANs and 802.1Q Tagging

![[Pasted image 20211122235921.png]]

The basics of 802.1Q trunks are as follows:

- Tagging is typically done on all VLANs.
- The use of a native VLAN was designed for legacy use (such as in the above example)
- Unless changed, VLAN1 is the native VLAN.
- Both ends of a trunk link must be configured with the same native VLAN.
- Each trunk is configured separately, so it is possible to have different native VLANs on separate trunks.

##### Voice VLAN Verification Example

![[Pasted image 20211123000054.png]]

The `show interfaces fa0/18 swutchport` command shows both data and 