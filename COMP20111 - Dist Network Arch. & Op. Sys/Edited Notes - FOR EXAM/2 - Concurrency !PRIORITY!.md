# Concurrency
Operating systems have **three** different architectural layers:
- Userland
	- APIs, syscalls
- Kernelspace
	- Drivers
	- System security
	- Configurations
	- I/O handling
	- Process scheduling
	- Interrupts
	- CPU synchronization
	- Kernelspace abstracts hardware, for compatibility.
- Bare-metal (hardware)
	- Microcode and software
		- BIOS
		- CPU
		- MMU, etc.

## Programs and Processes
- **Programs** are compiled sourcecode.
- **Processes** are instances of programs.
	- Can have **several processes** under the **same program**
		- Each has its own address space
			- Range of memory