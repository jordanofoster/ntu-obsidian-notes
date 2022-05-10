# Best Fit

![[BestFit.png]]

- Searches *entire list*, beginning-to-end
	- Attempts to find hole *closest to required size*
		- Intent is to *not* break up bigger holes
- In theory, *doesn't waste memory* ^c39139
	- Practically, generates many *useless [[Memory Partitioning#^a0233c|holes]]* compared to [[First Fit]]
- *Extremely slow*
	- *Entire list searched*