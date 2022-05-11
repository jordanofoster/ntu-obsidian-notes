#comp20111-dnaos/topic-4 
# File Systems

![[ParitionTable.png]]

- Drives are divided into partitions/volumes
	- Each holds an *independent filesystem*
	- In this example, section 0 is the *Master Boot Record (MBR)*
		- Boots the computer via a **boot block**
			- Stored in specified partition, from where OS is loadd
		- **Super block** contains partition info (e.g., number of blocks)

## File Block Allocation Methods

![[BlockAllocation.png]]

- Blocks are *subdivisions* of [[Non-Volatile Memory|mass storage]]
	- Similar to [[Paging|pages]] but in secondary memory

Objective of blo