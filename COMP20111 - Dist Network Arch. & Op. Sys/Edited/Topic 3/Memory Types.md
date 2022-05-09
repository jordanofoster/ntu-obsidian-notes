# Memory Types

## Volatile

Volatile memory *does not* retain information after power loss. Examples include:

- [[Memory Types#Processor Registers]]
- [[Memory Types#Cache Memory]]
- [[[Memory Types#Random Access Memory (RAM)]]]

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

- Small, slower than [[Memory Types#Processor Registers|registers]] but still fast
- Used to *reduce* average time/energy cost to access data from [[[Memory Types#Random Access Memory (RAM)|RAM]]
- Resides within CPU
	- Acts as intermediary between [[Memory Types#Processor Registers|registers]] and [[[Memory Types#Random Access Memory (RAM)|RAM]]
	- Modern CPUs have a *sub-hierarchy* of *Cache Levels*
		- Fastest-to-slowest, Lowest-to-highest
			- e.g. L1, L2, L3, L4 etc.
