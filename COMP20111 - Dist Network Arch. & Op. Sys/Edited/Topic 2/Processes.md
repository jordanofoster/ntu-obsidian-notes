#comp20111-dnaos/topic-2
# Processes

- Processes are running instances of a [[Programs|program]].
	- A single *flow of control* with a start and end. ^49d2fc
	- Only one *point of execution* at a given time. ^26a0a7
	- By default, one [[Threads|execution thread]].
- Each process has its own [[Memory Management#Address Spaces|address space]].
- Each process has a *Process Identification Number* (PID). ^a534ab

Multiple processes share [[Resources]]. ^dfcfe2
## Process Creation

There are two methods:
- Via **explicit** execution by user
- Via [[Spawning and Forking|Spawning/Forking.]]

## Process Tables

- Process tables keep track of [[Processes#^a534ab|PIDs]].
- Each process in the table has a *Process Control Block* (PCB).
	- These hold *Process Descriptors*:
		> ![[Process Descriptors.png]] ^7a999f

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