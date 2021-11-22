# Server Hardware and Software

##  Why use servers?

### Hardware

- Multiple enterprise-class processors
- Larger memory capacity
- High performance:
	- I/O, Networking capabilities
		- Tend to have leading-edge CPUs, high spec NICs and associated upgrade options.
- High availability
	- Servers need to last longer, so upgrades/spares need to be available for longer
- High extensibility
	- Room for more disks, cards, memory, fans...
- Components engineered to higher standards than consumer products
	- Servers want to be reliable as they have long uptime and heavier system demands:
		- Redundant PSUs, disks/disk controllers, hot-*swap* memory...
- Servers offer maintenance contracts; support is neccessary as they are typically business-critical.

### Software

- Main reason to run a server
- Desktop OSes often have a limited featureset
	- e.g. XP is limited to 10 concurrent connections (blocked HTTP)
	- Windows 7+/Vista - IIS 7.5 will queue requests for a limited number of connections at the same time, although connections can be from more machines.
	- Microsoft Terminal Services / RDS is limited to one connection at a time (third-party tools can circumvent this.)

#### Windows Server Versions

##### Windows Server 2022

Built on strong foundations of 2019, brings innovations on three themes; security, Azure hybrid integration and management/application platforms. WS2022 Datacenter: Azure Edition allows cloud servers to be used to keep VMs up to date while minimizing downtime.

##### Windows Server 2019

Built on 2016, offered innovations in the form of Hybrid Clouds, Security, new Application Platform, and Hyper-Converged Infrastructure (HCI).

###### Editions of 2019

- Essentials, for small businesses (25 users/50 devices); ideal first server, can also be used as primary server in multi-server environment
- Standard, limited to two Hyper-V containers - low density/non-virtualized environments. Added features like Nano Server/unlimited Windows Server containers.
- Datacentre, with increased network features and Hyper-V support; no container limit, shielded VMs, software defined-networking, Storage Spaces Direct, and Storage Replica.

##### Windows Server 2016

New Hyper-V support, Updated Nano server, offered shielded VMs and Cloud/Hybrid Active Directory Environments.

#### Ubuntu Server

- Runs all major architectures: x86-64, ARMv7, ARM64, POWER8, POWER9, IBM s390x (LinuxONE), RISC-V
- Latest stable 5.11 kernel for new hardware/security updates
- Offers Wireguard with modern crypto defaults and increased usability compared to OpenVPN
- AppArmor3 for more security
- LTS releases receive security updates for 5 years by default. Every 6 months, interim releases give new features; hardware enablement updates add support for latest machines to all supported LTS released.
- Ubuntu Advantage for Infrastructure subscriptions include Extended Security Maintenance which increases support lifecycle for up to 10 years.
- 21.04 gives new Hardware Enablement networking stack, extensions to live installed and APT phased updates. Improved enterprise applications availability - native MS SQL Server support on 20.04 LTS.

## Server/Comms Rooms & Cable Management

It is preferable to have a clean, lockable environment to keep servers in, using remote methods to control/monitor them but providing a local screen/keyboard just in case network issues arise.

Rack-mount systems are preferred, even if only one server is being used - as this allows easy extensibility/replacement.

Spares packs are sometimes provided for 	quick repairs, and cabling must be considered as the server infrastructure grows.

### Server Racks

Server racks help with the following:

###### Increasing Performance
- Proper airflow, if installed properly.
- Racks are customizable.
- Empty shelves can be removed and racks can be covered with blanking panels.

###### Increasing Security
- Locked panels to keep away intruders.

###### Ease of Maintenance

- All servers are together, and racks are mostly equipped with wheels and shelves that easily slide out, making it easier to access the server and maintain it - or resolve problems.

## Network Hierarchy
![[NtwrkHierarchy.png]]

Hierarchical networks use tiered designs of access, distribution and core layers, with each performing well-defined roles on the network.

### Access Layer

The access layer provides network access to the user, and connects to distribution layer switches.

### Distribution Layer

The distribution layer implementing routing, quality of service, and security measures. It does this by aggregating large-scale wiring closet networks and limiting Layer 2 broadcast domains. Distribution layer switches connect to access and core layer switches.

### Core Layer

The core layer acts as a network backbone, connecting several layers of the network together. It also provides fault isolation and high-speed connectivity.

### Three/Two-Tier Hierarchical Networks

These are two time-tested and proven design frameworks for campus networks.

#### Three-Tier

![[ThreeTierNtwrk.png]]

These are used by organizations requiring access, distribution and core layers. It is recommended to build an extended-star network topology from a centralised building location to all other locations on the same campus.

#### Two-tier

These are used when separate distribution/core layers are not required. They are useful for smaller locations, or sites consisting of a singular building.

They are also known as *collapsed core* network designs.


## Example of Hierarchical Network - NTU Infrastructure
###### Physical connections of LAN distribution switches/routers
Telecomms use JANET.
![[NTULanDiag.png]]

###### Clifton Distribution

A high-speed link exists between Clifton Campus and other networks. The datacentre is located in 005-005a, and contains 15 cabinet servers. Infrastructure itself is hidden, and each building has separate connections.
![[NTUCliftonDiag.png]]

The infrastructure present on NTUs campuses represent a very large system; ones of this scale tend to grow and occasionally are prone to re-engineering rather than a complete redesign from scratch.