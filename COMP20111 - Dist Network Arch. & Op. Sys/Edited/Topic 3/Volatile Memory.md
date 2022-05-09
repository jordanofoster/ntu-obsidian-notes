# Volatile Memory

Volatile memory *does not* retain information after power loss. Examples include:

- [[Volatile Memory#Processor Registers|Registers]]
- [[Volatile Memory#Cache Memory|Cache]]
- [[Volatile Memory#Random Access Memory RAM|RAM]]

### Processor Registers

- Small and extremely fast
- Reside within CPU
	- Typically as single containers that hold one value
- Typically referred to by name rather than *address*
- Used primary for *arithmetic operations*
- Manipulated/tested by *machine instructions*

There are two types of register; *generic* and *specialised.*

![[GenericSpecialisedRegisters.png]]

 - *Generic Registers* are used to store *function* data:
	 - *Parameters*
	 - *Outputs*
- *Specialised Registers* are for *specific purposes*
	- Typically named as such - e.g. *program counter*

### Cache Memory
![[CacheDiagram.png]]

- Small, slower than [[Volatile Memory#Processor Registers|registers]] but still fast
- Used to *reduce* average time/energy cost to access data from [[Volatile Memory#Random Access Memory RAM|RAM]] 
- Resides within CPU:
	>![[CPU-ZExample.png]]
- Acts as intermediary between [[Volatile Memory#Processor Registers|registers]] and [[[Memory Types#Random Access Memory (RAM)|RAM]]
	- Modern CPUs have a *sub-hierarchy* of *Cache Levels*
		- Fastest-to-slowest, Lowest-to-highest
			- e.g. L1, L2, L3, L4 etc.

### Random Access Memory (RAM)

A diagram that connects RAM to CPU registers/cache is shown below:

![[MainMemoryRAMDiagram.png]]