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

## Distributed Synchronisation
For distributed systems, we have to remember that the systems are formed out of a number of machines working together.

![[Pasted image 20220328121421.png]]

There are a few considerations to be made in instances where some machines are dependent on others;
1) Is the system using synchronous or asynchronous messaging?
2) Do we block when waiting for a reply (RPC?)
3) How do we detect and recover from failures?
4) How can we enforce mutual exclusion in a distributed context?

### Distributed Mutual Exclusion
On a single machine, we can use semaphores or other shared variable to protect shared resources. With distributed systems, such methods cannot be relied upon - we need to consider a message passing system to relay this information.

There are a few things we must consider when making a distributed mutual exclusion mechanism; firstly, we must consider the application-level protocol for a critical section:

![[Pasted image 20220328122204.png]]

We also need to consider some other requirements:
1) Only one process can run in the critical section at a time.
2) Any requests to enter or exit the critical section will eventually succeed.
3) The order in which requests are received are adhered to (e.g. FIFO)

#### Central Server Algorithm
This is the simplest form of enforcing mutual exclusion, where the server acts as a central system, maintaining and coordinating access.
![[Pasted image 20220328122519.png]]

There are two other methods; ring-based, and multicast & logical clocks. We could also use *Elections.*

#### Ring-based Algorithm
This is a simple method for controlling *mutual exclusion* without the need for a central system.