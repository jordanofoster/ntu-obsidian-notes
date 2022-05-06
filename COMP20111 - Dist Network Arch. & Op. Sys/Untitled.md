# Programs and Processes
- **Programs** are compiled source code
- **Processes** are running *instances* of programs
	- Several *instances* (or processes) of a program can run simultaneously
			- Each *process* has its own **address space** of memory.

## Process Creation
- Processes can be made by:
	- A **user** (through explicit **execution**)
	- **Another process**
		- This is called **spawning/forking**
		- A **parent** process spawns a **child** process.
			- If the child **becomes a parent,** it ma