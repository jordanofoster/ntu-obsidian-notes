#comp20111-dnaos/topic-3 
# Placement Policies

![[LinkedList.png]]

[[Tracking Free Space#Tracking Free Space in Volatile Memory Main Memory comp20111-dnaos topic-3|Linked Lists]] keep track of [[Processes|processes]] and [[Memory Partitioning#^a0233c|memory holes]] sorted by [[Memory Management#Address Spaces|address]]. *Placement Policies* help efficiently allocate memory for *new [[Processes|processes]]*, and define behaviour when deciding between several [[Memory Partitioning#^a0233c|compatible memory holes]]. They are listed as follows:

- [[First Fit]]
- [[Next Fit]]
- [[Best Fit]]
- [[Worst Fit]]
- [[Quick Fit]]