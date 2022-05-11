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

- Blocks are *subdivisions* of [[Non-Volatile Memory|mass storage]] ^a97394
	- Similar to [[Paging|pages]] but in secondary memory

- File block allocation tracks which files go to *which block* on a [[Non-Volatile Memory#Hard Drives isys20231-nda topic-4|disk]]
	- Different schemes to achieve this
		- [[Contiguous File Block Allocation]]
		- [[Linked-List File Block Allocation (Non-Contiguous)]]
			- [[Linked List with File Allocation Table (FAT)]]
		- [[i-nodes]]

## Determining Block Size

- [[File Systems#File Block Allocation Methods|All allocation methods]] require the disk to be split into *fixed-size [[File Systems#^a97394|blocks]]* - almost *all modern systems* use blocks as such.
	- Trade-off is similar to [[Segmentation#Comparison of Paging and Segmentation|page size]] in [[Memory Management]]:
		- With sm