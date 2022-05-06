# Programs and Processes
- **Programs** are compiled source code
- **Processes** are running ***instances* of programs**
	- Several *instances* (or processes) of a program can **run simultaneously**
			- Each *process* has its own **address space** of memory.

## Process Creation
- Processes can be made by:
	- A **user** (through explicit **execution**)
	- **Another process** through **spawning/forking.**
		- A **parent** process spawns a **child** process.
			- If the child **becomes a parent,** it makes a **process tree.**

## Process Table
- Processes are given a **Process Identification Number** (**PID**)
	- This is stored in a *process table* by the OS
	- Each entry has a **Process Control Block** (**PCB**)
		- a PCB holds **Process Descriptors**

![[Process Descriptors.png]]

## Process States
- There are **three:**
	- **RUNNING** on the CPU
	- **READY** and waiting on CPU
	- **BLOCKED** by unavailable resources
- Processes are in *resource queues*
	- Each queue represents a *specific resource*
		- 