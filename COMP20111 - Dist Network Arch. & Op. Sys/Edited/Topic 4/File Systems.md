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
		- With small block sizes, files occupy several blocks
			- Longer access time as *more blocks must be located*
				- Thus, *greater overhead*
		- With large block sizes:
			- A small file (e.g. 1KB) *wastes space*, by requiring a block larger than it (i.e. 32KB).
	- Typical block sizes are therefore used (512B/1KB/2KB).

## Consistency

- File systems read/modify/write blocks
	- If they *crash* before all modifications are written, errors can occur!
		- This is *inconsistency.*
			- Most OSs offer programs to deal with this:
				- UNIX has `fsck`
				- Windows has `chkdsk`

An example diagram detailing [[File Systems|filesystem]] states is shown:

![[ConsistencyDiag.png]]

- `(a)` - Consistent.
- `(b)` - *Missing* [[File Systems#^a97394|block]]
- `(c)` - Duplicate [[File Systems#^a97394|block]] in free list.
- `(d)` - Duplicate *data* [[File Systems#^a97394|block]]

## Journaling

- Single file operations sometimes require *multiple disk writes.* 
	- Using UNIX as an example:
		1) Remove [[Files|file]] from [[Directories and Folders|directory]]
		2) Release [[i-nodes|file i-node]] to list of *free i-nodes*
		3) Return all [[Non-Volatile Memory#Hard Drives isys20231-nda topic-4|disk]] [[File Systems#^a97394|blocks]] to pool of *free blocks*
	- Similar steps required in Windows
- Issues can occur with an error
	- If `1)` completes and then the system crashes:
		- The [[i-nodes|i-node]] and [[Files|file]] [[File Systems#^a97394|blocks]] are not accessible *from any file*
			- Or available for reassignment!
	- Fixing this requires time-consuming repair (e.g., `scandisk`, etc.)

![[JournalingExample.png]]

- *Journaling* filesystems use part of the disk to *log* pending [[File Operations]]
	- Under failure, the *log* helps bring disk back to [[File Systems#Consistency|consistency]]
		- i.e. by completing all pending actions.
- Log entries are erased upon successful completion

## Security in File Systems

- File access can be managed through *Access Control Lists*
	- Each object (e.g. [[Files|file]]) contains a list of principles
		- These determine what can be done:
	- 