# RAID (Redundant Array of Inexpensive Disks) #comp20111-dnaos/topic-4 

- [[Non-Volatile Memory#Hard Drives isys20231-nda topic-4|Disks]] (excluding SSDs) are a system bottleneck
	- RAID mitigates this by *distributing data* across several *physical* disks
		- Appears as a single *logical* disk
			- Adds another layer of *abstraction*
- RAID provides many performance/reliability benefits
	- Depending on implementation:
		- RAID 0 (Striping):
			- Distributes data across *several disks*
				- Improves speed, gives *full capacity*
					- No *'security* whatsoever.
		- RAID 1 (Mirroring):
			- Uses *more than one disk* to store *the same data*
				- Degrades speed, *doesn't ensure full capacity*
					- But ensures data security
		- RAID 1+0 takes advantage of both:
			- ![[RAID1+0.png]]
