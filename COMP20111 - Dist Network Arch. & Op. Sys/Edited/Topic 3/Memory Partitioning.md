#comp20111-dnaos/topic-3 
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
	- Each partition has unused space - *internal fragmentation* ^76d30b
		- Because of this, may not be a partition big enough to fit a [[Processes|process]]

## Variable Partition Memory

![[VarPartMem.png]]

- [[Processes]] are allocated *exactly* what they need
	- Then loaded into *contiguous* memory slots until full.
- Advantages:
	- No *internal fragmentation*
	- Space *freed* when [[Processes|processes]] terminate
	- Adjacent fragmentations *mergeable*
	- *Unfixed* number of [[Multithreading|parallel]] [[Processes|processes]]
- Disadvantages
	- Assumes [[Memory Management Unit (MMU)|memory manager]] knows required memory for [[Processes|process]]
		- Can cause memory holes *outside* of partition - *external fragmentation*  ^b913a9
			- This can be resolved with [[Compaction]].