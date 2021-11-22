# Introduction to Operating Systems
## History of Operating Systems

- In the late 1950s, standard subroutines were made to load on start-up; these were the first sign of an OS-like feature
	- Magnetic tapes were first used for storage, followed by disks; **Assembly** appeared, followed by **FORTRAN**
- The automated batch system (**punch-card**) was developed in the 1960s
	- Programs were loaded into memory in a **First-In-First-Out** (FIFO) style
- **Multiprogramming** was introduced in the 1970s
	- Systems could now switch between jobs, allowing processing and I/O to occur seemingly at once
- 1980s - **GUIs appear**, multi-user systems and concurrency become mainstream **due to Unix**
- 1990s - **Networking becomes mainstream** alongside more secure OSes (Windows NT)

## Centralised computing
- Centralised computers have a **local set of resources** (including memory, a processor, I/O ports, graphics capability and storage medium)
	- They are **fully shareable** and **connected tightly** with the use of one unifying OS.
	- **General computers (PCs, Laptops, Tablets, etc.)** are classed as such, containing many hardware components.
		- These components are accessible to the processor through the **motherboard** - all internal components are connected via **data buses,** and **interfaces for connecting peripherals** are also included.

## Operating Systems
- Operating Systems are **collections of system programs** that **manage hardware resources** and **connected peripherals.**

Operating systems have two complementary functions:
	- **Management of resources**
	- **Machine extending**
		- This refers to the abstraction of hardware issues from user consideration.

They also provide the following practical features:
	- **Concurrency** (Performing several operations/computations at once)
	- **Shareable hardware resources**
	- **Long term storage access**
	- **Non-determinacy,** which is being resilient to unpredictable events without crashing.
	
### Why have operating systems?
Operating systems:
- **Remove accessibility boundaries for the less technically inclined**
	- They do this by eliminating the percieved boundary between **hardware** and the **software it runs...**
	- And by providing an easy-to-use environment to **develop and run programs.**

### Architecture
Operating systems have **four main component management subsystems:**
	- **Process**
	- **Memory**
	- **I/O**
	- **File management**
	
Subsystems can also exist for **security, networking and GUIs.**

Operating system components are best modelled as **layers;** each provides functionality to those above it, and **uses functionality derived from within or below its current layer.**

In most OSes, only the **top layer** is visible to the user. This may either be a GUI or a command prompt.

### Kernel and Usermode
Operating systems themselves are part of the kernel and run in **kernel mode.** This essentially allows **complete control of the hardware** through execution of privileged instructions.

Non-kernel level software run in **usermode/userland;** this means that they can **only use certain functions.** No control over the machine itself is given, with the exception of some via **syscalls** - these are unique to each OS and often limited.

#### Why the distinction?
- A user/programmer with full access could be capable of using **as many resources as they wish.**
	- Useful in some cases, but mostly could cause system errors.

Following the rule that programmers generally are terrible at producing bug-free software, usermode acts as a safety net when a program inevitably fails in some manner.

Without this, **kernel errors** could occur - and these tend to be fatal to the system as a whole.

## Distributed Systems
- Distributed systems are **isolated networks** of **multiple autonomous computers.**
- Each computer has its **own CPU and memory.**
- **Middleware** is used to connect these systems together **through a network** in a process known as **message passing,** although each individual device will also contain it's **own OS.**
	- As a result, to understand the workings of distributed systems, **an understanding of standard OSes is also required.**
	- Distributed systems also face **many of the same issues** that traditional OSes face, **including but not limited to:**
		- *Synchronisation*
		- *Coordination*
		- *Distributed Memory*
		- *Distributed File Systems*
		-  *Resource Allocation*
		-  *Concurrency*
	- They also face **their own issues:**
		- *Infrastructures and Models*
		- *Messaging Systems*
		- *Coordination and Synchronisation*
		- *Designing software systems that can run over several systems*
		- *Storage and* ***Security***

## Parallel Computing
- Modern systems now either contain **multiple cores** or **multiple computers.**
- These allow different programs to be run alongside eachother **simultaneously** via a process known as **Parallelisation.**
	- This is a **major component** of systems that is **scalable up to any level,** including large scale and distributed computing; as a result, **Parallelisation presents the same problems to all systems.**

### How does it work?
In parallel computing all processing nodes in a machine can be linked in **two different ways:**

![[Clusters.png]]
	- Tightly coupled, **sharing memory:**
		-  Nodes have the same specifications, OS and Network config but share memory.

![[TightlyCoupled.png]]
	- Loosely coupled with **distributed memory** (Clusters):
		- Nodes are identical as before, but each node has its own private memory with addressable space. 

Considerations:
	- Inter-processor communication (shared/message parsing)
	- Concurrency in allocating/processing packets of work.
	
	