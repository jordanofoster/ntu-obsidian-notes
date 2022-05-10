# First Fit

![[FirstFit.png]]

- Searches from *beginning* for **first hole big enough** for *new [[Processes|process]]*
	- It is then *split* into *used* and *unused* [[Memory Management#Address Spaces|space]]
- Statistically *unlikely* to have a perfect fit
	- May end up making *even more [[Memory Partitioning#^a0233c|holes]]*
- Fast - because we're *trying to minimize* search-time