# Virtualization

A virtual machine (VM), also called a guest machine, is a software simulation of a hardware platform that provides a virtual operating environment, for guest operating systems.
*platform* - or system/full virtualization VMs - run on top of hypervisors, and simulate a complete hardware platform.

Application/process VMs instead run as a language-specific software application (such as a Java VM) on top of the host OS, providing a platform-independent programming environment.

## Virtualisation Hypervisors

![[Pasted image 20220214132550.png]]

Hypervisors, also known as Virtual Machine Monitors (VMMs), are software programs that run on actual host hardware platforms, and supervise the execution of guest OS code on the VMs.

### Notional Diagram Type 1 ("Bare Metal" Hypervisor)

![[Pasted image 20220214132625.png]]

### Notional Diagram Type 2 ("Hosted" Hypervisor)

![[Pasted image 20220214132651.png]]

## Current Virtualization Trends

Virutalization is reaching saturation point at the server level for IT applications, data centres, and cloud computing. However it is increasingly being used for mass storage (via storage virtualization), Network virtualization and for Mobile devices (mainly for testing on virtual mobile devices).

Virtualization is only just beginning to see use in real-time, safety-critical and security-critical systems, such as Automotives, IoT and Millitary niches.

Virtualization is also being combined with virtualization; where appropriate, full-fat VMs are replaced by lighter containers. As a side effect, security is increasingly important; as vulnerabilities (VM escapes) in virtual machines and hypervisors are discovered.

## Pros and Cons of Virtualization

### Pros

#### Increased Hardware Isolation

Virtualization supports the reuse of software written for different (potentially old) operating systems and hardware. Additionally, the tech enables the upgrade of obsolete hardware infrastructure software, and improves the portability of software to multiple hardware/OS platforms.

Finally, the virtualization of testbeds is also possible.

### Decreased Hardware Costs

This is through enabling of consolidation, or the allocation of multiple applications to the same hardware device. This allows us to do the following:
- Take advantage of multicore hardware architecture
- Replace several lightly-loaded machines with fewer, more heavily-loaded machines to achieve the following:
	- Minimise SWAP-C (size, weight, power and cooling)
	- Free up hardware for new functionality
	- Support load balancing

Virtualization also supports cloud computing, server farms and mobile computing

### Optimizations

Virtualization software can be optimized for general purpose computing, such as MIS and cloud computing. This maximizes the throughput adn average case response time. Virtualized systems are, however, not optimized for some other things:
	
- Embedded real-time/safety-critical/cyber-physical systems
- Meeting deadlines

Virtualization may also improve operational availability by supporting failover and recovery, alongside the enabling of dynamic resource management.

## Spatial/Temporal Isolation of VMs

Hypervisors significantly improve (but do not guarantee) the *spatial* and *temporal* isolation of VMs. 

*Physical/Spatial Isolation* means that different VMs are prevented from accessing the same physical memory locations, such as caches and RAM. *Temporal* isolation means that the execution of software on one VM does not impact the temporal behaviour of software running on another VM.

Achieving spatial and temporal isolation improves the following:
- Reliability and Robustness
	- Localizing the impact of defects to a single VM
	- Enabling software failover and recovery
- Safety
	- By localizing impact of faults/failures to a single VM
- Security
	- By localizing impact of malware to a single VM

## Security

As stated before, spatial isolation largely limits the impact of malware to a single VM. It should be noted however that 

