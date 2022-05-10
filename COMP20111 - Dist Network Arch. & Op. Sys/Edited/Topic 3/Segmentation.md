#comp20111-dnaos/topic-3 
# Segmentation

Segmentation is a [[Memory Management]] scheme that works alongside the *user-view* of [[Programs|programs]]. Each is split into *segments* of variable size, according to its *logical structure:*

![[SegmentationDiagram.png]] ^f1c0fb
- A `C` compiler may have *4 segments*, as shown above - all of *different sizes.*

[[Processes]] have memory allocated segment-by-segment, in *non-[[Contiguous Memory Allocation|contiguous]]* areas of [[Memory Management#Memory Without Abstraction|physical memory]]. Each segment has its *own [[Memory Management#Logical Address Spaces|address space]]*. 

Segmentation properties are enumerated thus:

- Segmentation allows for *logical division* of programs
	- Segments can *grow and shrink* independently (e.g., [Stack](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)) and [Heap](https://en.wikipedia.org/wiki/Heap_(data_structure))). 
- Allows for [[Segmentation#Protection and Sharing with Segmentation|protection and sharing]] 
- Segments are typically *larger* than [[Paging|pages]] and may waste space
	- Additionally prone to [[Memory Partitioning#^a0233c|external fragmentation]]

## Protection and Sharing with Segmentation

- [Protection]() is achieved by:
	- Assigning modes (read/write/execute) to each segment
	- Checking that memory references do not *exceed* segment length
- [Sharing]() refers to a shared segment that is referenced by multiple [[Processes|processes]]
	- Such as a [library]()

## Comparison of [[Paging]] and [[Segmentation]]

- [[Paging]] allows more [[Memory Management#Logical Address Spaces|addressable space]] without *actual* [[Volatile Memory#Random Access Memory RAM|physical memory]].
	- Memory is divided in a way that is *transparent* to the user
	- But pages are *fixed-size* 
		- Offset by having *no [[Memory Partitioning#^b913a9|external fragmentation]]* 

- [[Segmentation]] allows [[Programs|programs]] to be broken up into independent [[Memory Management#Logical Address Spaces|logical address spaces]], allowing [[Segmentation#^f1c0fb|logical division]], which is *visible to the user*
	- This is *useful for programmers*
- Segments are of a *variable size*
	- Nice for efficiency; can generate [[Memory Partitioning#^b913a9|memory holes]]

## [[Segmentation]] with [[Paging]]

- Segments are larger than pages.
	- Can present a problem is segment is larger than [[Memory Management#Memory Without Abstraction|physical memory]].
		- Can be resolved by *mapping* [[Segmentation|segments]] into [[Paging#^ea0e56|page frames]] via *paging segments*
			- Each segment is assigned with a page table, achieving the *best of both worlds:*
				- **Avoiding [[Memory Partitioning#^b913a9|external fragmentation]]**
				- **Aids [sharing]() and [protection]()** 
				- **Supports *user-view* of program**

The combination of the two is roughly equivalent to modern [[Memory Management]] techniques, as seen in x86, ARM and others.