#comp20111-dnaos/topic-4 
# Contiguous File Block Allocation

![[ContigAlloc.png]]

- Simple implementation
	- Only stores *first block address* and its *length*
- Very performant
	- Ease of [[File Access#^174f37|random access]]
- Robustness against [[Non-Volatile Memory#Hard Drives isys20231-nda topic-4|disk]] faults
	- Damage to a single block only causes *localised damage*
- Initial file size *must be tracked*
	- Files themselves *cannot grow*
		- e.g., document cannot have data [[File Operations#^558d90|appended]]
- [[Memory Partitioning^frag]]