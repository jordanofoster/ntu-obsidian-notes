#comp20111-dnaos/topic-3 
# "Not Frequently Used" Page Replacement

Tracks page usage by associating each page with a *counter*, initially set to `0`.

1) At each [[Interrupts#^46cbff|clock interrupt]], OS scans *all pages in memory*
2) For each page, [[Paging#^bec2a7|reference]] bit is added to associated counter.
	- Counters track how often pages are referenced.
3) When page faults occur, page with *lowest counter* is replaced.

Almost *full* utilisation of [[Memory Management#Memory Without Abstraction|physical memory]] is achieved, and there is also *no* [[Memory Partitioning#^a0233c|external fragmentation]]. Some costs, however:

- Some [[Memory Partitioning#^76d30b|internal fragmentation]].
	- Processes cannot use memory in *multiples* of a page.
		- e.g., Last page usually *does not* use the entire page size.
- *Tuning* allocated page size is difficult:
	- Smaller page sizes reduce [[Memory Partitioning#^76d30b|internal fragmentation]]...
		- ...But require larger [[Paging#Page Tables|paging tables]]
	- Larger page sizes means *more unused programs* are loaded into memory...
		- ...But smaller [[Paging#Page Tables|paging tables]]

Having one [[Paging#Page Tables|page table]] per [[Processes|process]] consumes *lots* of [[Memory Management#Memory Without Abstraction|physical memory]], and this method does not *divide pages into units* to support *[[Segmentation|logical division]]* of [[Programs|programs]]. 