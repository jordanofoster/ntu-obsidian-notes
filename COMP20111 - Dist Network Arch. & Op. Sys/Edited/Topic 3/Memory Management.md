# Memory Management

[[Processes]] share physical memory as well as CPU time. Instructions are fetched from [[Volatile Memory#Random Access Memory RAM|main memory]] and handed to the CPU for [[Fetch-Execute Cycle|execution]]; main memory is large enough to store *several* running processes at once.

![[MemMgmtDiagram.png]]

Therefore, we must use [[Memory Management]] for concurrent processes by taking advantage of [[Locality of Reference]] - moving frequently used data up the [[Memory Hierarchy|hierarchy]]. We also do the following:
- Protect [[Processes|processes]] from using each other's memory
- Relocate memory to *new* [[Processes|processes]]
- Overall make memory addressing transparent through [[Memory Management#Memory Abstraction|abstraction]].

## Memory Abstraction

![[AbstractionDiagram.png]]

Similar to creating an [[Concurrency|abstract CPU that runs processes 'concurrently']], management systems provide *abstract memory* that allows the coexistence of [[Processes|processes]] inside [[Volatile Memory#Random Access Memory RAM|physical]] [[Non-Volatile Memory#Hard Drives|memory]].

### Address Spaces

These are sets of *address locations* that reference specific parts of physical memory.

![[LogAddrSpaces.png]]

*Logical* address spaces have programmers refer to their *own* address space; the issue being how we differentiate between the same *logical* address on separate [[Processes|processes]] (as each maps to a *unique* physical address).

[[Programs]] are *loaded*
## Memory Without Abstraction

>![[NonAbstractionDiagram.png]]
- *`c` is an example of the memory layout MS-DOS used for the OS component stored in the BIOS.*

In early systems, every [[Programs|program]] could access physical memory. Programmers were given a direct set of addresses, with each corresponding to a fixed bit-length cell. There are obvious disadvantages:

- *Impossible* to run *more than one program* [[Scheduling|at the same time]]
	- When one program is loaded over another, instructions are overwritten.
- [[Concurrency]] *is* possible with [[Threads|threads]]...
	- But this only allows us to run *[[Threads#^b4cb70|related processes]]*.

### Referencing Physical Memory

- Within some OSes, memory can be addressed *directly*:
>	![[ReferencingPhysMem.png]]

- This can result in the OS being damaged accidentally or intentionally.
- Additionally, it can be difficult to run multiple programs using [[Scheduling#Context Switching|context switches]].