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

#### Decreased Hardware Costs

This is through enabling of consolidation, or the allocation of multiple applications to the same hardware device. This allows us to do the following:
- Take advantage of multicore hardware architecture
- Replace several lightly-loaded machines with fewer, more heavily-loaded machines to achieve the following:
	- Minimise SWAP-C (size, weight, power and cooling)
	- Free up hardware for new functionality
	- Support load balancing

Virtualization also supports cloud computing, server farms and mobile computing

#### Optimizations

Virtualization software can be optimized for general purpose computing, such as MIS and cloud computing. This maximizes the throughput adn average case response time. Virtualized systems are, however, not optimized for some other things:
	
- Embedded real-time/safety-critical/cyber-physical systems
- Meeting deadlines

Virtualization may also improve operational availability by supporting failover and recovery, alongside the enabling of dynamic resource management.

#### Spatial/Temporal Isolation of VMs

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

#### Security through Isolation

As stated before, spatial isolation largely limits the impact of malware to a single VM. It should be noted however that sophisticated exploits can escape from one VM to another (via the hypervisor).

Compromised VMs can be terminated and replaced with a new VM, booted from a clean image. This enables a rapid system restore or software reload following a cybersecurity compromise.

Bare-metal Type 1 hypervisors have a relatively small attack suface, being less subject to common OS exploits and malware. Security software and rules implemented at the hypervisor level can also apply to all of its VMs.

### Cons

#### Increased Hardware Resource Requirements

VMs and hypervisors require more CPU strength, and greater amounts of RAM. Images (of software state/date) require increased amounts of storage. Virtualization can simulationously increase and decrease the required amount of hardware, dependant on requirements. Architecture engineering typically determine which of these trends dominate.

#### Sharing of Resources

VMs share a Hypervisor, Host OS, and some other shared resources within multicore processors:
- Processor-internal resources (L3 cache, system bus, memory and I/O controllers and interconnects)
- Processor-external resources (main memory, I/O devices and networks)

The sharing of resources imply several potential issues:
- Singular points of failure
- The possibility for two applications running on the same VM to interfere with eachother
	- Additionally, software running on one VM can impact software running on another VM; primarily of the sort that violates temporal isolation.

#### More difficult Interference Analysis

Analysis of temporal interference (such as meeting timing deadlines) is difficult and typically results are overly conservative. Additionally, interference analysis becomes more complex with an increase in the number of VMs, and when virtualization becomes concerned with multicore processing.

The number of potential interference paths increase rapidly with the number of VMs; exhaustive analysis of all paths is typically impossible, meaning representative selection of paths is neccessary.

#### Safety Recertification & Related Issues

Moving to virtualized architectures based on hypervisors/VMs will likely require safety recertification.

Furthermore, interference between VMs can cause missed deadlines and excessive jitter. Faults (hazards) and failures (accidents) can occur, and as stated before, interference requires proper real-time scheduling and timing analysis.

Safety policy guidelines are based on obsolete assumptions, and need to be updated. Safety-critical applications can be run on multiple VMs, achieving software redundancy with voting.

#### Security Recertification & Related Issues

Moving to a virtualized architecture based on hypervisors and virtual machines will probably require security recertification. Security vulnerabilities can also violate isolation, as sophisticated exploits can escape from one VM to another, via the hypervisor.

#### Increased risk of Concurrency Defects

Concurrency defects can be more likely to occur due to VMs executing concurrently, on one or more cores. These defects are listed as follows:
- [Deadlocks]([Deadlock - Wikipedia](https://en.wikipedia.org/wiki/Deadlock))
- [Livelocks]([Deadlock - Wikipedia](https://en.wikipedia.org/wiki/Deadlock#Livelock))
- [Starvation](https://en.wikipedia.org/wiki/Starvation_(computer_science))
- [Suspension](https://en.wikipedia.org/wiki/Lock_(computer_science)#Granularity)
- [(Data-based) race conditions](https://en.wikipedia.org/wiki/Race_condition#Data_race)
- [Priority inversion](https://en.wikipedia.org/wiki/Priority_inversion)
- Order violations
- Order vulnerabilities
- [Atomicity violations](https://en.wikipedia.org/wiki/Atomicity_(database_systems))

Additionally, virtualization increases the amount and difficulty of testing for concurrency defects.

#### Stability

A lack of real-time predictability causes jitter and failure to meet hard real-time deadlines due to response time, Additionally, virtualization is a relatively new technology, and hypervisors and VMs as a result tend to be more buggy than operating systems. When integrating and testing new virtualized systems, an increased number of test cases is required, causing an increase in duration of the testing phase. These include:

- [Reliability testing](https://en.wikipedia.org/wiki/Software_reliability_testing)
- [Soak testing](https://en.wikipedia.org/wiki/Soak_testing)
- [Reliability Demonstration Testing](http://www.gmr-solutions.com/reliability-services/reliability-demonstration-testing/reliability-demonstration-testing-rdt/)
- [Accelerated life testing](https://en.wikipedia.org/wiki/Accelerated_life_testing)

#### Increased Licensing Costs

This is, naturally, avoided if using FOSS software.

## Containers

Containers are virtual runtime environments that run on top of a single OS kernel, without any attempt to emulate the underlying hardware. a *pod* as a cohesive collection of containers that are co-located and share resources.

Containerization is sometimes called *virtualization via containers*. However the following distinction must be made: *Virtualization* refers to multiple virtual *hardware platforms*, whereas *Containerization* refers to multiple virtual *operating systems.*

Containerization itself is the process of engineering a software architecture with the use of multiple containers. Container orchestration - by extension - refers to the process of managing (e.g. creating/deploying/securing/monitoring) multiple containers; possibly spread across multiple VMs/cores/processors/clusters.

### Diagram of "Pure" Containerization

![[Pasted image 20220214144856.png]]

#### Diagram of Virtualization combined with Containerization

![[Pasted image 20220214144916.png]]


### The Container Lifecycle
Typically, the lifecycle of a container consists of three phases; 

1) The container is created, tested and accredited
2) Images are made of the container, to be stored and retrieved as needed
3) Containers are deployed and managed

The diagram below helps visualize this idea:
![[Pasted image 20220214145054.png]]

### Current Container Trends

Containers are becoming more common in recent years because they provide many of the isolation benefits of VMs, without causing as much overhead. Although they are typically hosted on some version of Linux, containers are beginning to also be hosted on other OSes such as Windows.

Containers are heavily used in cloud-hosted applications, and are increasingly leveraged to support the continuous development and integration (CD/CI) of containerized microservices.

## Pros and Cons of Containers

### Pros

#### Lightweight Spatial and Temporal Isolation

Each container is provided with its own resources (e.g. CPU and memory) and container-specific namespaces. The overhead of this is less than VMs, as containers do not emulate underlying hardware.

#### Easy instantiation at scale

Multiple individual containers are relatively easily instantiated, enabling the support of scalability, availability/reliability (via redundancy/failover), and load balancing.

#### Support for continuous procecedure

Containers have support for DevOps and continuous integration/deployment (CI/CD).

#### Environmental/Timing Consistency

Containers provide consistency between development/test/operational environments, and have more consistent timing than VMs, meaning that containers can have real-time and safety applications.

#### Decreased code size

Container applications can share binaries and libraries, and this is the main benefit of such design. Shared binaries/libraries can also cause issues however (this will be covered in Cons).

### Cons

#### Cons shared with VMs

##### Sharing of Resources

Containers share a *lot* compared to VMs:
- The container engine and OS kernel
- VM
- Hypervisor
- Host OS (if container in VM running type 2 hypervisor)
- ...on top of the resources VMs share:
	- Processor-internal resources and Processor-external resources

###### Why resource sharing is bad

Their implementation implies shared single points of failure, and increased risk ofm interference:
- Applications running in the same container can interfere with each other.
- Applications running in one container can potentially impact software in another container, as interference has potential to violate spatial and temporal isolation.

##### Difficulty of Interference Analysis

Same as VMs, the analysis of interference (particularly temporal) is difficult, and outcomes are typically overly conservative - additionally, containerization is always combined with virtualizationa and multicore processing, meaning containers will *always* adopt the exponential difficulty of analysis that they cause.

#### Increased Concurrency Defects

Containers are prone to increased concurrency defects, much like VMs, and suffer the same knock-on effects.

### Security

Containers are typically insecure by default and require significant hardening:
- No data can be stored inside the container's pattern.
- Container processes must be forced to write to container-specific filesystems
- Container network namespaces must be made to write to specific private intranets.
- Container services should have thier privileges minimized (i.e. non-root, if possible)

Additionally, moving to a containerized architecture could require recertification. The [NIST Application Container Security Guide (SP 800-190)](https://doi.org/10.6028/NIST.SP.800-190) is written to assist with this.

### Additional Restrictions

Containers are largely restricted to Linux-based operating systems; container sprawl (excessive containerization) increases the need for management.

## Tabular Summarization of Lecture

### When to use what - Multicore computers, VMs or Containers

| Criteria | Multicore | Virtualization | Containerization |
| --- | :---: | :---: | :---: |
| Reliability and Robustness | Yes | Yes | Yes |
| Concurrency | Yes | Yes | Yes |
| Temporal and Spatial Isolation | Yes | Yes | Yes |
| Configurability (flexible deployment) | Yes | Yes | Yes |
| SWAP-C | Yes | Yes/No | Yes |
| Portability (Multiple HW Platforms) | No | Yes | No |
| Portability (Multiple OSes) | No | Yes | No |
| Technology Refresh | Yes | Yes | Yes |
| Legacy Software Reuse | Somewhat | Yes | Somewhat |
| Performance (throughput) | Yes | Somewhat | Yes |
| Hard real-time (response time) | Somewhat | No | Somewhat |
| Safety | Somewhat | Improved | Improved |
| Security | Somewhat | Improved | Less Improved |

### Comparison of VMs and Containers

| Criteria | VMs | Containers |
| --- | :---: | :---: |
| Portability (\# of operating systems) | One or more per HV | One/ContainerEng |
| Portability (\# of OS versions) | One or more per HV | One or more per CE |
| Portability (\# of OS types) | One or more | Primarily Linux |
| Security (roughly equal, depending on use) | Improved isolation | Improvded isolation, smaller attack surface |
| \# of applications per server | Lower | Higher |
| \# of copies of single application | One | Many |
| Performance (throughput, not response time) | Lower | Higher |
| Overhead (administration) | Higher | Lower |
| Overhead (resource usage) | Much higher | Much lower |
| Readily share resources? (devices, services) | No | Yes |
| Robustness (via failover/restart) | Not supported | Supported |
| Scalability/load balancing (dynamic deployment) | Slower and harder | Faster and easier |
| Application runs on bare metal | Not supported | May be supported |