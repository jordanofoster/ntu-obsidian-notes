# "Not Frequently Used" Page Replacement

Tracks page usage by associating each page with a *counter*, initially set to `0`.

1) At each [[Interrupts#^46cbff|clock interrupt]], OS scans *all pages in memory*
2) For each page, [[Paging#^bec2a7|reference]] bit is added to associated counter.
	- Counters track how often pages are referenced.
3) When page faults occur, page with *lowest counter* is replaced.

Almost *full* utilisation of [[Memory Management#Memory Without Abstraction|physical memory]] is achieved - to the point wh