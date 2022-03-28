# Co-ordination, Scheduling and Resource Management

## Why do we need it?
**Coordination** is required so that a master coordinates activities within a cluster or system; any node can be the coordinator.

**Synchronisation** is needed because shared resources can be used. As a result, policies for dealing with distributed mutual exclusion is required.

**Scheduling**/load balancing methods are needed for dealing with workloads on individual nodes.

There are two types of algorithms for synchronisation, coordination and scheduling; those that are **centralised** and those that are **decentralised.**

There are also other issues we must consider:
- Best topology to use
- Best messaging system (IPC)
- Distributed Memory
- Clocks (as seen in topic 10)

## Recap on Shared Resources
Critical sections are enforced using a construct called a [[Topic 2 - Concurrency#Semaphores|semaphore.]] This is used to guard resources, and was initially inspired from railroads, being the original inspiration for Dijkstra's algorithm. On singular machines, shared resources must be accessed; we use critical sections via semaphores to provide this mutual exclusion.

![[Pasted image 20220328121247.png]]

