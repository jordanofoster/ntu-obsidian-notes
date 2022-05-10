# Paging

This is a [[Memory Management]] mechanism that allows *non*-[[Contiguous Memory Allocation|contiguous]] allocation by dividing [[Memory Management#Memory Without Abstraction|physical memory]] and [[Memory Management#Logical Address Spaces|logical address spaces]] into *equal-size* blocks, called *frames* and *pages* respectively.

![[PagingDiagram.png]]

*Pages* are loaded into available *frames* as the [[Processes|processes]] contained are [[Programs#Program Execution|executed]]; the process counters [[Memory Partitioning#^a0233c|external fragmentation]] - much like [[Compaction]].

## Forming Pages

![[FormPageProcDiagram.png]]

- Each [[Memory Management#Logical Address Spaces|logical address]] has a [[Processes|process]] *page number* $(s)$ and *displacement or offset* $(d)$ within that page. ^8d6b7e
- Each [[Processes|process]] has a *page table* that records the *frame number* for each *[[Processes|process]] page*.
	- This is implemented in hardware, using the [[Memory Management Unit (MMU)|MMU]].

### Example 1

![[FrmPgProcDiagramEx1.png]]

- With 16-bit [[Programs|program]]/[[Processes|process]] address of `0100 0000 0110 0100`:
	- $s$ (4-bits) is `0100` or 4.
	- $d$ (12-bits) is `0000 0110 0100`
- Physical address:
	- `1100 0000 0000 0000` + `0000 0110 0100` = `1100 0000 0110 0100`$_2$

### Example 2

![[FrmPgProcDiagramEx2.png]]

- With 16-bit [[Programs|program]]/[[Processes|process]] address of `0101 0110 0110 0101`:
	- $s$ (4-bits) is `0101` or 5.
	- $d$ (12-bits) is `0110 0110 0101`
- Physical address:
	- `1011 0000 0000 0000` + `0000 0110 0110 0101` = `1011 0110 0110 0101`$_2$

## Page Tables

These map *virtual pages* into *page frames*. Their layout is *highly machine dependent* but some common fields persist:

1) **Page frame**
	- This defines the *frame number.*
2) **Present**
	- This defines whether a page is *present* in [[Volatile Memory#Random Access Memory RAM|main]] or [[Non-Volatile Memory#Hard Drives|secondary]] memory.
3) **Modified**
	- This records whether a page is *modified* since its last loading.
		- This is also called a *dirty bit* - if true (`1`), the page *must be copied back to [[Non-Volatile Memory#Hard Drives|disk]]*.
4) **Protection**
	- Records what kind of *access* (Read/Write/Execute) is permitted.
5) **Referenced**
	1) 