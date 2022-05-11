#comp20111-dnaos/topic-4 
# Linked List with [File Allocation Table (FAT)](https://en.wikipedia.org/wiki/Design_of_the_FAT_file_system)

![[LLFAT.png]]

- Used by older versions of MS-DOS/Windows
- Improves upon [[Linked-List File Block Allocation (Non-Contiguous)|basic linked-list allocation]] with a [*file allocation table* (FAT)](https://en.wikipedia.org/wiki/Design_of_the_FAT_file_system) that stores *all pointers in memory* 
	- Standardized in different ways - e.g., [FAT16](https://en.wikipedia.org/wiki/File_Allocation_Table#Initial_FAT16) and [FAT32](https://en.wikipedia.org/wiki/File_Allocation_Table#FAT32)
- FAT must be in [[Volatile Memory#Random Access Memory RAM|memory]] *at all times*
	- To get a file, we point to the location in the FAT...
		- ...that contains the [[Memory Management#Logical Address Spaces|memory address]] of the *first block*
- Frees up space otherwise occupied by [[Linked-List File Block Allocation (Non-Contiguous)#^4cc555|block-specific pointers]]
	- Pointers stored in faster [[Volatile Memory|main memory]]
		- [[File Access#^174f37|Random access]] is *much quicker* than [[Linked-List File Block Allocation (Non-Contiguous)|standard LL]]
- [[File Types#^5c8c03|Drive references]] not required
- FAT may get *too large*
	- Especially for [[Non-Volatile Memory#Hard Drives isys20231-nda topic-4|drives]] with high capacity
- Damage to FAT causes *serious data loss*
	- Can be rectified with backups