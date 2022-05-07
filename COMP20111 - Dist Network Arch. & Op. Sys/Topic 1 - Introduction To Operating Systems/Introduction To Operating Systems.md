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

- Other processes are **User** mode
	- Restricted functionality
	- Machine control provided via *syscalls*
	- Safety net for bad programs
		- But less available resources

