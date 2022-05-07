# Processes

- Processes are running instances of a [[Program|program]].
- Each process has its own [[Address spaces|address space]].
- Each process has a *Process Identification Number* (PID). ^a534ab

## Process Creation

There are two methods:
- Via **explicit** execution by user
- Via [[Spawning+Forking|Spawning/Forking.]]

### Process Tables

- Process tables keep track of [[Processes#^a534ab|PIDs]].
- Each process in the table has a *Process Control Block* (PCB).
	- These hold *Process Descriptors*:
		> ![[Process Descriptors.png]]

### Process States

There are three:
- currently **RUNNING**
	- One process **at a time**
- **READY** for execution
	- Queued with others in same state
- **BLOCKED** 