# Paging

This is a [[Memory Management]] mechanism that allows *non*-[[Contiguous Memory Allocation|contiguous]] allocation by dividing [[Memory Management#Memory Without Abstraction|physical memory]] and [[Memory Management#Logical Address Spaces|logical address spaces]] into *equal-size* blocks, called *frames* and *pages* respectively.

![[PagingDiagram.png]]

*Pages* are loaded into available *frames* as the [[Processes|processes]] contained are [[Programs#Program Execution|executed]]; the process counters [[Memory Partitioning#^a0233c|external fragmentation]] - much like [[Compaction]].

## Forming Pages

![[FormPageProcDiagram.png]]

- Each [[Memory Management#Logical Address Spaces|logical address]] has a [[Processes|process]]