# Segmentation

Segmentation is a [[Memory Management]] scheme that works alongside the *user-view* of [[Programs|programs]]. Each is split into *segments* of variable size, according to its *logical structure:*

![[SegmentationDiagram.png]]
- A `C` compiler may have *4 segments*, as shown above - all of *different sizes.*

[[Processes]] have memory allocated segment-by-segment, in *non-[[Contiguous Memory Allocation|contiguous]]* areas of [[Memory Management#Memory Without Abstraction|physical memory]]. Each segment has its *own [[Memory Management#Logical Address Spaces|address space]]*. 

Segmentation properties are enumerated thus:

- Segmentation allows for *logical division* of programs
	- Segments can *grow and shrink* independently (e.g., [Stack](https://en.wikipedia.org/wiki/Stack_(abstract_data_type)) and [Heap](https://en.wikipedia.org/wiki/Heap_(data_structure))). 
- Allows for [[Protection and Sharing with Segmentation|protection and sharing]] 
- Segments are typically *larger* than [[Paging|pages]] and may waste space
	- Additionally prone to [[Memory Partitioning#^a0233c|external fragmentation]]