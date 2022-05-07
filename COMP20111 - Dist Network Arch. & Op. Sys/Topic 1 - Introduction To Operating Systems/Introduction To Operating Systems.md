# Centralised Computing
- Centralized systems include PCs, laptops, etc.
	- Have **local resources** that are **CPU accessible**
		- **Fully shareable,** connected via OS
		-  Connected to **CPU** through **motherboard**
			- Internal components - via **data buses**
			- External peripherals - via **interfaces**

# Operating Systems
- **Collections of programs** that manage:
	- **Hardware resources**
	- **Connected peripherals**
	
- They provide:
	- **Resource Management**
	- **Machine extending**
		- *Abstraction of hardware from user*
	- **Concurrency
		- Several operations "simultaneously"
	- **Shared hardware resources**
	- **Long-term storage**
	- **Non-determinacy**
		- *Resistance to crashes from unpredicted events*
		- See *Byzantine Fault Tolerance*

- Removes **accessibility boundaries** from less technically literate
	- No boundary between *hardware/software*
	- Easy-to-use development/runtime environments

## OS Architecture
- **Four main management subsystems**
	- Process
	- Memory
	- I/O
	- File Management
- Additional subsystems for:
	- Security
	- Networking
	- GUIs

- OSs are **built in layers**
	- Assist layers above
	- Use layers below
	- Only top layer user-visible

### Kernel and Usermode
- OS software is **Kernel** mode
	- *Complete control of hardware
	- Errors are **fatal**

- Other processes are **User** mode
	- Restricted functionality
		- Safety net for bad programs
		- Machine control provided via *syscalls*

# Distributed Systems
- **Isolated networks** of **multiple autonomous systems**
	- Each has its own resources and OS
	- Connected via **middleware**
		- Uses **message passing** over network
- Similar issues to *centralized:*
	- **Synchronization**
	- **Coordination**
	- **Distributed Memory**
	- **Distributed Filesystems**
	- **Resource Allocation**
	- **Concurrency**
- Also unique issues:
	- **Infrastructures/Models**
	- **Messaging Systems**
	- **Coordination/Synchronization**
	- **Requires specific software**
	- **Storage and Security**