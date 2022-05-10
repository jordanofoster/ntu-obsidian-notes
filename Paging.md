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
2) **Present** ^dc1948
	- This defines whether a page is *present* in [[Volatile Memory#Random Access Memory RAM|main]] or [[Non-Volatile Memory#Hard Drives|secondary]] memory.
3) **Modified** ^621b28
	- This records whether a page is *modified* since its last loading.
		- This is also called a *dirty bit* - if true (`1`), the page *must be copied back to [[Non-Volatile Memory#Hard Drives|disk]]*.
4) **Protection**
	- Records what kind of *access* (Read/Write/Execute) is permitted.
5) **Referenced** ^bec2a7
	- OS sets this when page is used.

## Page Fault Handling

*Page faults* occur when part of a [[Processes|process]] is *not* in [[Volatile Memory#Random Access Memory RAM|main memory]] when [[Fetch-Execute Cycle|needed by the CPU.]] This causes an [[Interrupts|interrupt]]:

1) OS selects existing page frame
2) Page's [[Paging#^621b28|modified]] bit is checked for modifications.
	- If `1`, write contents back to [[Non-Volatile Memory#Hard Drives|disk]].
3) Fetch a new page from the [[Non-Volatile Memory#Hard Drives|disk]], discarding the old page in the *frame.* ^86a515
4) Update page/frame mappings and *restart* the trapped instruction.
	- Mark the *virtual page* as *unmapped* (using the *[[Paging#^dc1948|present]] bit*) and update the address to [[Paging#^86a515|that page]] with a new [[Memory Management#Memory Without Abstraction|physical address]].

When [[Processes|processes]] terminate, all related pages are *released* from [[Virtual Memory|virtual memory]].

## Page Replacement

Here, we must decide which *page* to remove from [[Volatile Memory#Random Access Memory RAM|RAM]] and place within [[Non-Volatile Memory#Hard Drives|mass storage]] - *efficiently* and with *minimal overhead.* [[Thrashing]] is of particular concern, and so we should consider the following, using information from the [[Paging#Page Tables|page table]]:

1) [[Paging#^621b28|Modified]] pages must *first be saved*
	- *Unmodified* pages are simply overwritable.
2) Avoid replacing *often-used pages* - **both** in and out of [[Volatile Memory#Random Access Memory RAM|main memory]].

Optimally, we replace pages that are *not needed* for the *longest period of time*, but this is infeasible:

1) It is *impossible* to know a program's *future*
2) Thus; *impossible* to know *when* a page is next needed.

[[Page Replacement Algorithms]] are still useful despite this, as they use predictors.