# Tracking Free Space

## Tracking Free Space in [[Volatile Memory|Main Memory]] #comp20111-dnaos/topic-3 

![[FreeSpaceMgmt.png]]

Two methods exist:
- Bitmaps - Figure `(b)`
- Linked Lists - Figure `(c)` ^d9cbd3

## Tracking Free Space in [[File Systems]] #comp20111-dnaos/topic-4 

### Linked List Method

![[TrackFreeSpaceLLMethod.png]]

- Some leftover free blocks hold the *number* of free [[Non-Volatile Memory#Hard Drives isys20231-nda topic-4|disk]] [[File Systems#^a97394|blocks]]
	- These are *linked* together, making their *own linked list* of free blocks
- Overhead percentage *lowers* as drive fills ^b984f5

### Bitmap Method
![[TrackFreeSpaceBMMethod.png]]
- Bitmaps are stored with *one bit/block* that records if it is free or used:
	- `1` - free
	- `0` - used
- Occupy less space than [[|Linked Lists]]
	- 1 bit/block vs. 32 bits
	- Number of blocks required to track free space is *constant*, unlike [[Tracking Free Space#^b984f5|Linked Lists]]