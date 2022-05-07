# Processes

- Processes are running instances of a [[Program|program]].
- Each process has its own [[Address spaces|address space]].
- Each process has a *Process Identification Number* (PID). ^a534ab

## Process Creation

There are two methods:
- Via **explicit** execution by user
- Via [[Spawning+Forking|Spawning/Forking.]]

## Process Tables

- Process tables keep track of [[Processes#^a534ab|PIDs]].
- Each process in the table has a *Process Control Block* (PCB).
	- These hold *Process Descriptors*:
		> ![[Process Descriptors.png]]

## Process States

There are three:
- currently **RUNNING** ^555d69
	- One process **at a time**
- **READY** for execution ^bb9c04
- **BLOCKED** by busy resources ^1436ce

### Process Queues

**[[Processes#^bb9c04|READY]]** and **[[Processes#^1436ce|BLOCKED]]** processes are in respective queues:
>![[StateQueue.png]]

## Process Termination

- **Voluntary**
	- **Normal exit** - work finished
	- **Error exit** - error handled during execution
- **Involuntary**
	- **Fatal error** - OS detected, illegal operation
	- **Killed** - by another process - via OS syscall