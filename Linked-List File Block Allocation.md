#comp20111-dnaos/topic-4 
# Linked-List File Block Allocation

- Files stored as *Linked-List* of blocks
	- First bytes of each block used as pointer
		- Each block contains its own data and a pointer to the next
			- Final block has *null* pointer.
- *Every block usable*
- File sizes *don't need to be known*
	- Allows *growth*
- *No fragmentation*
	- Excluding last block
		- Can have [[Memory Partitioning#^76d30b|internal fragmentation]]
- [[File Access#^174f37|Random access]] *unsupported*
	- Method is *very slow* - must traverse a *chain of blocks*
- Data overhead in form of block pointers