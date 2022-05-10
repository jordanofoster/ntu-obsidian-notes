#comp20111-dnaos/topic-3 
# Distributed Shared Memory

![[DistSharedMem.png]]

- Single computer systems have discrete resources available - CPU(s), Memory, Bus, I/O, etc.
	- In distributed systems, each node has discrete resources, but they link together to form a whole.
		- Memory is one such resource that requires marshalling, be it for use individually or collectively.
			- [[Distributed Shared Memory (DSM)]] is based on [[Message Passing]].