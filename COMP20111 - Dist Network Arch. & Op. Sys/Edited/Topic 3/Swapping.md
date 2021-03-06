#comp20111-dnaos/topic-3 
# Swapping

Memory is *not infinite* (see the [[Memory Hierarchy]]) and [[Processes|processes]] often need more [[Volatile Memory#Random Access Memory RAM|RAM]] as a collective than is available. To solve this, *idle [[Processes|processes]]* are typically stored on [[Non-Volatile Memory#Hard Drives|Secondary Memory]] to save [[Volatile Memory#Random Access Memory RAM|RAM]].

![[SwappingDiagram.png]]

*Swapping* involves bringing in *each* [[Processes|process]] [[Contiguous Memory Allocation|entirely]], giving it [[Programs#Program Execution|execution time]] and then returning it to *mass storage.* It acts much like [[Scheduling#Context Switching|context switching]] within [[Memory Management|memory management]]. Swapping (much like [[Compaction|compaction]]) requires overhead - typically by the OS having to [[Tracking Free Space|track free space]].