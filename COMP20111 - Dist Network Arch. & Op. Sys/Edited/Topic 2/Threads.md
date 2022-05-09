#comp20111-dnaos/topic-2
# Threads

Threads are *independent* execution paths/sequences within a [[Processes|process]], and are a key construct in [[Multithreading|multithreaded]] [[Programs|applications]]. 

New threads are stored in a [[Processes#Process Tables|Thread Control Block (TCB)]] upon creation. They share other similarities with processes:
- [[Processes#^49d2fc|Flow of Control]]
- Single [[Processes#^26a0a7|Point of Execution]]
- [[Processes#Process States|States]]
- [[Scheduling#Context Switching|Context Switching]]
- [[Spawning and Forking|Spawning/Forking]]

But differences too:
- Only existent *within* a [[Processes|process]] ^b4cb70
	- [[Spawning and Forking|created/controlled]] by an existing process
- Share [[Memory Management#Address Spaces|address space]] with parent
	- Creating/[[Scheduling#Context Switching|Switching]] is *inexpensive* as a result.
- Also share some of parent's [[Processes#^7a999f|properties]]
	- But have their own private *Thread Descriptors* too:
		> ![[ProcessThreadBlock.png]]

Multiple threads share [[Memory Management#Address Spaces|address space]], in contrast to [[Processes#^dfcfe2|processes]].

## User Threads

- Typically created/managed by *user-level library* *without kernel knowledge*
	- Fast to create/manage
	- Portable to any OS
- If *one thread* is blocked, all are. ^5bfc61

## Kernel Threads

- Directly managed/supported by kernel
- Have inverse properties of [[Threads#User Threads|user threads]]:
	- Slower to create/manage
	- OS-specific
	- Threads are treated independently ([[Threads#^5bfc61|unlike user threads]]) ^efd154
-  Allows parallelism on *multiple CPUs*