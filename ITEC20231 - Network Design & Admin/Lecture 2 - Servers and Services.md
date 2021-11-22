# Servers and Services

## Networks
A network is a group of interconnected computers. In businesses, computers enhance inter-human communications, speed up routing tasks, and improve human decision making. Networks, being infrastructures of connected computers, facilitate this even moreso.

### Client/Server model

These days, the client/server model is tended to with the following elements:
- Client - A PC with a GUI (runs programs)
- Server - more power PC, provides services (e.g. databases/other applications)
- Physical Network - PAN/LAN/MAN/WAN
- Logical Connections - The 'glue' that connects clients to services.

#### Servers vs. Clients

##### Server Roles

- File Server
	- Central Storage and Backup Control
- Print Server
	- Job spooling and usage tracking
- Application Server
	- Provides web services (e.g. IIS, Apache) and Databases (MS SQL Server, MySQL)
- Mail Server
- DNS Server
- DHCP Server
- Domain Controller
	- Active Directory Domain
	- Central Administration
- Terminal Services server
- Remote Desktop Infrastructure
- Remote Access / VPN Server
- Hyper-V Server
- Media Streaming Server

###### Domain Controller

A domain controller provides centralised control of users and controls access to network resources (such as shares, printers, etc.)
Microsoft-based  servers can be promoted to domain controllers easily, through the use of Active Directory - in AD Domain Services, they hold a copy of the ADDS database itself.

Ther are also other non-windows Domain Controllers, such as Samba and Red Hat FreeIPA.

Domain Controllers are extremely important, and redundancy is implemented in the form of having several up at once.

###### Dynamic Host Configuration Protocol (DHCP)

DHCP servers allocate IP addresses to local devices on the network upon request. This works as follows:

1. The client machine boots and broadcasts a DNS Discovery query as it searches for the servrer.
2. The server reserves an IP for the client, sending it as a DHCP offer.
3. The client can take the IP as an offer, and must tell any other DHCP servers prsent of this offer via another broadcast DHCP request that includes the IP of the server making an offer.
4. At this point, other DHCP server cancel their offers to the same client, returning the offered IP address to the pool; the server with the accepted offer completes the process by sending a DHCP ACK message to the client, with additional info such as IP lease expiry time.

It should be noted that Discovery and Request broadcasts must be made to inform other DHCP servers that may be listening of the state of the transaction.

The client itself is not aware of the addresses of any DHCP servers, so broadcasts are required over the physical subnet to find them. Network admins may optionally allow DHCP traffic to be forwarded by the router towards another subnet.

There are a few variants of address allocation:
- Dynamic; the address is allocated for a lease period from the pool, being reused after the lease expires.
- Automatic; the address is assigned permanently to the client, with the client getting preferential access to that IP the next time it makes a request.
- Static; a list of MAC/IP address pair is manually assigned to the client.

Windows server makes use of DHCPv6, which can assign both IPv4 and IPv6 addresses.

Assignment of addresses is automatically done via auto-configuration. This can allocate addresses one of three ways:

- Stateless
- Stateful
- Both

In large networks, it is typical to have more than one DHCP server. As a result, address ranges need to be configured such that they overlap - this allows all addresses to be available even if one server goes down. This does, however, introduce the risk of IP conflicts. This can be resolved via one of the following:

- DHCP Server Conflict Resolution
- Using non-overlapping address ranges
- Client starts an Address Resolution Probe (ARP) to validate its assigned address

###### Domain Name System

Originally, networks were very small, so manual lists of machines and their addresses on each host were maintained alongside a central list file at a particular server. It still exists as etc/hosts on both Linux and Windows systems. However, this is obviously unrealistic for large dynamic networks such as the internet - server need to work out IP addresses, given a domain (which are used as a humanly memorable name for a machine).

In the event that nameservers to not exist, some servers can survive by broadcast queries, but software to resolve names against addresses have existed since 1983. The tree structure of domain names allows a client to find out an address by sending domain name requests up the tree. DNS server try to resolve requests from a client (although clients sometimes cache recently resolved names). If they cannot resolve it themselves, they pass it on up the tree - Bind is a standard open-sourcee implementation in this regard.

DNS and DHCP as a collective link MAC, IPs and domain names together.

![[DomainNameSys.png]]

#### Network Operating Systems
These consist of the likes of Windows 10 and Windows Server 2019. Their base is the NT Kernel architecture - kernels are bridges between user applications and hardware, and help to manage computer resources such as processes, memory and device management.

Kernels act as a Hardware Abstraction Layer (HAL) - these act as a layer between hardware and operating system, and typically have hardware specific code (or drivers).

Linux systems have similar concepts to windows systems, but name them differently, such as having a *board support package*.


##### Windows Architecture
![[WindowsArch.png]]

Above is a representation of the architecture of Windows systems, based on the NT kernel. There are two main components; usermode and kernelmode. 32-bit and 64-bit support is present over the Windows API, which is available in all operating systems using the same kernel. Win32 is the 32-bit variant, Win64 is the 64-bit variant.

Programs and other subsystems that run in usermode have limited access to system resources. User-mode subsystems include:

- Enviroment subsystems, which run applications
- The integral subsystem, which operates system-specific functions on behalf of the environment subsystems.

The kernel sits between the HAL and Executive services, providing multiprocessor synchronization, thread/interrupt scheduling and dispatching alongside trap handling. It is also responsible for initialising device drivers at bootup required for the system to run. 

Kernel mode itself has unrestricted access to system memory and connected external devices. The executive service interfaces with all user-mode subsystems, and manages I/O, objects, security and processes. These functions are divided into several subsystems.

##### GNU/Linux Architecture

![[GNULinuxArch.png]]

Much like windows, GNU/Linux systems have a user-mode in the form of userspace, where applications are executed. These systems make large use of the GNU C Library, *glibc*, which provides a syscall interface that connects to the kernel and provides mechanisms to travel between user-space applications and kernel-space systems. 

The system call inteface is also responsible for process management; memory is formed into *pages*, segments that are typically 4KB in size for most architectures. Linux includes the means to manage available pages, as well as hardware-supported mechanisms for both physical and virtual mappings.

Similarly, Virtual File Systems (VFSs) are an aspect of the Linux kernel that provides a common abstraction interface for file systems.

At the top of the diagram the syscall interface implements basic functions such as read/write - below that, kernel code exists; this is common to all CPU arches supported by Linux.

Below architecture-agnostic code, architecture-dependent code exists - also known as a Board Support Package (BSP). This code facilitates processing and use of platform-specific code for the given architecture.





