# Memory Partitioning

## Fixed Partition Memory

![[FixedPartMem.png]]

- Memory divided into partitions of *fixed size*
	- Not all are the *same size*, but they cannot grow or shrink
- Each process is given its own fixed partition to work with
- Advantages:
	- Compatible with [[Processes|process]] coexistence - allows multiprogramming
	- Easily implemented
	- Fast [[Scheduling#Context Switching|context switching]]
- Disadvantages:
	- Restricted number of simultaneous [[Processes|processes]]
	- Each partition has unused space - caused *internal fragmentation*
		- Because of this, may not be a partition big enough to fit a [[Processes|process]]