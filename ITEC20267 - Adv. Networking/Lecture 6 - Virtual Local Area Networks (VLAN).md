# Virtual Local Area Networks (VLAN)

`This lecture replicates Cisco online teaching materials.`

## Definition of a VLAN

![[VLANDiag.png]]

VLANs are logical connections with other similar devices; placing devices into various VLANs have the following characteristics:
- Provides segmentation of the various groups of devices on the same switches
- Provides organizations with more manageable networks:
	- Broadcasts, multicasts and unicasts are isolated within the individual VLAN
	- Each VLAN has its own unique range of IP addressing
	- Smaller broadcast domains

### Benefits of a VLAN

![[VLANDiag2.png]]

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

### VLAN Identification with a Tag

![[Pasted image 20211122235133.png]]

The IEE 802.1Q header is 4 bytes long. When the tag is created, the FCS must be recalculated. When sent to end devices, this tag must be removed and the FCS recalculated back to its original number.

| 802.1Q VLAN Tag Field | Function |
| --------------------- | -------- |
| Type | 2-Byte field with hexadecimal `0x8100`. This is referred to as the Tag Protocool ID (TPID). |
| User Priority | 3-bit value that supports `note: blank here? fill later` |
| Canonical Format Identifier (CFI) | 1-bit value that can support token ring frames on Ethernet |
| VLAN ID (VID) | 12-bit VLAN identifier that can support up to 4096 VLANs |

#### Native VLANs and 802.1Q Tagging

![[Pasted image 20211122235921.png]]

The basics of 802.1Q trunks are as follows:

- Tagging is typically done on all VLANs.
- The use of a native VLAN was designed for legacy use (such as in the above example)
- Unless changed, VLAN1 is the native VLAN.
- Both ends of a trunk link must be configured with the same native VLAN.
- Each trunk is configured separately, so it is possible to have different native VLANs on separate trunks.

#### Voice VLAN Verification Example

![[Pasted image 20211123000054.png]]

The `show interfaces fa0/18 swutchport` command shows both data and voice VLANs assigned to the interface.

### VLAN Ranges on Catalyst Switches

![[Pasted image 20211123000243.png]]

Catalyst switches 2960 and 3650 support over 4000 VLANs.

| Normal Range VLAN (1 - 1005) | Extended Range VLAN (1006 - 4095) |
| ---------------------------- | --------------------------------- |
| Used in Small to Medium sized businesses | Used by Service Providers |
| 1002 - 1005 are reserved for legacy VLANs | Are in Running-Config |
| 1, 1002 - 1005 are auto-created and cannot be deleted | Supports fewer VLAN features |
| Stored in the vlan.dat file in flash | Requires VTP configurations |
| VTP can synchronize between switches | |

### VLAN Creation Commands

VLAN details are stored in the `vlan.dat` file. VLANs are created in the global configuration mode.

| Task | IOS Command |
| ---  | ----------- |
| Enter global configuration mode | `Switch# configure terminal` |
| Create a VLAN with a valid ID number | `Switch(config)# vlan <vlan-id>` |
| Specify a unique name to identify the VLAN | `Switch(config-vlan)# name <vlan-name>` |
| Return to privileged EXEC mode | `Switch(config-vlan)# end` |
| Enter global configuration mode | `Switch# configure terminal` |

#### VLAN Creation Example

![[Pasted image 20211123000801.png]]

| Prompt | Command |
| ------ | ------- |
| `S1#` | `configure terminal` |
| `S1(config)#` | `vlan 20` |
| `S1(config-vlan)#` | `name student` |
| `S1(config-vlan)#` | `end` |

If the student PC is going to be in VLAN 20, we create the VLAN first and then name it. If you do not name it, the Cisco IOS will give it a default name of `vlan` and the four digit number of the VLAN (e.g. `vlan0020` for VLAN 20).

### VLAN Port Assignment Commands

Once the VLAN is created, it can then be assigned to the correct interfaces:

| Task | Command |
| ---  | ------- |
| Enter global configuration mode | `Switch# configure terminal` |
| Enter interface configuration mode | `Switch(config)# interface <interface-id>` |
| Set the port to access mode | `Switch(config-if)# switchport mode access` |
| Assign the port to a VLAN | `Switch(config-if)# switchport access vlan <vlan-id>`
| Return to privileged EXEC mode | `Switch(config-if)# end` |

#### VLAN Port Assignment Example

![[Pasted image 20211123001252.png]]

| Prompt | Command |
| ------ | ------- |
| `S1#` | `configure terminal` |
| `S1(config)#` | `interface fa0/18` |
| `S1(config-if)#` | `switchport mode access` |
| `S1(config-if)#` | `switchport access vlan 20` |
| `S1(config-if)#` | `end` |

We can assign the VLAN to the port interface. Once the device is assigned to the VLAN, the end device then needs the IP address information for that VLAN. Here, Student PC recieves `172.17.20.22`.

## Data and Voice VLANs

![[Pasted image 20211123001600.png]]

An access port may only be assigned to one data VLAN and one voice VLAN; the latter for when a phone and an end device are off of the same switchport.

### Trunk Configuration Commands

These are to configure and verify VLAN trunks. Trunks are layer 2 and carry traffic for all VLANs.

| Task | IOS Command |
| ---  | ----------- |
| Enter global configuration mode | `Switch# configure terminal` |
| Enter interface configuration mode | `Switch(config)# interface <interface-id>` |
| Set the port to permanent trunking mode | `Switch(config-if)# switchport mode trunk` |
| Sets the native VLAN to something other than VLAN 1 | `Switch(config-if)# switchport trunk native vlan <vlan-id>`
| Specify the list of VLANs to be allowed on the trunk link | `Switch(config-if)# switchport trunk allowed vlan <vlan-list>`
| Return to privileged EXEC mode | `Switch(config-if)# end` |

#### Trunk Configuration Example

![[Pasted image 20211123001900.png]]

| Prompt | Command |
| ------ | ------- |
| `S1(config)#` | `interface fa0/18` |
| `S1(config-if)#` | `switchport mode trunk` |
| `S1(config-if)#` | `switchport trunk native vlan 99` |
| `S1(config-if)#` | `switchport trunk allowed vlan 10,20,30,99` |
| `S1(config-if)#` | `end` |

The subnets associated with each VLAN are as follows:

- VLAN 10 (Faculty/Staff) - `172.17.10.0/24`
- VLAN 20 (Students) - `172.17.20.0/24`
- VLAN 30 (Guests) - `172.17.30.0/24`
- VLAN 99 (Native) - `172.17.99.0/24`

The `F0/1` port on S1 is configured as a trunk port.

Note: This assumes a 2960 switch using 802.1Q tagging. Layer 3 switches require the encapsulation to be configured before the trunk mode.

#### Introduction to DTP

The Dynamic Trunking Protocol (DTP) is proprietary and designed by Cisco. Its characteristics are as follows:

- On by default on Catalyst 2960/2950 switches
- Dynamic-auto is default on 2960/2950 switches
- May be turned off with the `nonegotiate` command
- May be turned back on by setting the interface to dynamic-auto
- Setting a switch to a static trunk or static access will avoid negotiation issues with the `switchport mode trunk` or `switchport mode access` commands.

![[Pasted image 20211123002557.png]]
![[Pasted image 20211123002601.png]]

##### Negotiated Interface Modes

The `switchport mode` command has additional options. The `switchport nonegotiate` interface configuration command can be used to stop DTP negotation.

| Option | Description |
| ------ | ----------- |
| `access` | Permanent access mode and negotiates to convert the neighboring link into an access link |
| `dynamic auto` | Will become a trunk interface if the neighboring interface is set to `trunk` or `desirable` mode |
| `dynamic desirable` | Actively seeks to become a trunk by negotiating with other `auto` or `desirable` interfaces |
| `trunk` | Permanent trunking mode and negotiates to convert the neighboring link into a trunk link |

